<a name="top"></a>
# <%= project.name %> v<%= project.version %>

<%= project.description %>

<% groupOrder.forEach(function (group) { -%>
- [<%= group %>](#<%=: group | mlink %>)
    <% nameOrder[group].forEach(function (sub) { -%>
- [<%= data[group][sub][0].name %>](#<%=: data[group][sub][0].name | mlink %>)
    <% }); -%>

<% }); %>

<% if (prepend) { -%>
<%- prepend %>
<% } -%>
<% groupOrder.forEach(function (group) { -%>
# <%= group %>

<% nameOrder[group].forEach(function (sub) { -%>
## <%= data[group][sub][0].name %>
<%= data[group][sub][0].title %>

<%-: data[group][sub][0].description | undef %>

    <%-: data[group][sub][0].type | upcase %> <%= data[group][sub][0].url %>

<% if (data[group][sub][0].header && data[group][sub][0].header.fields.Header) { -%>


### Headers

| Name    | Type      | Description                          |
|---------|-----------|--------------------------------------|
<% data[group][sub][0].header.fields.Header.forEach(function (header) { -%>
| <%- header.field %> | <%- header.type %> | <%- header.optional ? '**optional**' : '' %><%- header.description %>|
<% }); //forech parameter -%>
<% } //if parameters -%>

<% if (data[group][sub][0].header && data[group][sub][0].header.examples) { -%>

### Header Examples

<% data[group][sub][0].header.examples.forEach(function (example) { -%>
```json
<%- example.content %>
```
<% }); //foreach example -%>
<% } //if example -%>

<% if (data[group][sub][0].parameter) { -%>

<% Object.keys(data[group][sub][0].parameter.fields).forEach(function(g) { -%>

### Parameters

| Name     | Type       | Description                           |
|:---------|:-----------|:--------------------------------------|
<% data[group][sub][0].parameter.fields[g].forEach(function (param) { -%>
| <%- param.field %> | <%- param.type %> | <%- param.optional ? '**optional**' : '' %><%- param.description -%>
<% if (param.defaultValue) { -%>
_Default value: <%= param.defaultValue %>_<br><% } -%>
<% if (param.size) { -%>
_Size range: <%- param.size %>_<br><% } -%>
<% if (param.allowedValues) { -%>
_Allowed values: <%- param.allowedValues %>_<% } %>|
<% }); //forech (group) parameter -%>
<% }); //forech param parameter -%>
<% } //if parameters -%>

<% if (data[group][sub][0].parameter && data[group][sub][0].parameter.examples.length) { -%>


### Parameter Examples

<% data[group][sub][0].parameter.examples.forEach(function (example) { -%>
```json
<%- example.content %>
```
<% }); //foreach example -%>
<% } //if example -%>

<% if (data[group][sub][0].success && data[group][sub][0].success.examples && data[group][sub][0].success.examples.length) { -%>
### Success Response

<% data[group][sub][0].success.examples.forEach(function (example) { -%>
<%= example.title %>

```json
<%- example.content %>
```
<% }); //foreach success example -%>
<% } //if examples -%>

<% if (data[group][sub][0].success && data[group][sub][0].success.fields) { -%>
<% Object.keys(data[group][sub][0].success.fields).forEach(function(g) { -%>
### <%= g %>

| Name     | Type       | Description                           |
|:---------|:-----------|:--------------------------------------|
<% data[group][sub][0].success.fields[g].forEach(function (param) { -%>
| <%- param.field %> | <%- param.type %> | <%- param.optional ? '**optional**' : '' %><%- param.description -%>
<% if (param.defaultValue) { -%>
_Default value: <%- param.defaultValue %>_<br><% } -%>
<% if (param.size) { -%>
_Size range: <%- param.size -%>_<br><% } -%>
<% if (param.allowedValues) { -%>
_Allowed values: <%- param.allowedValues %>_<% } %>|
<% }); //forech (group) parameter -%>
<% }); //forech field -%>
<% } //if success.fields -%>

<% if (data[group][sub][0].error && data[group][sub][0].error.examples && data[group][sub][0].error.examples.length) { -%>
### Error Response

<% data[group][sub][0].error.examples.forEach(function (example) { -%>
<%= example.title %>

```json
<%- example.content %>
```
<% }); //foreach error example -%>
<% } //if examples -%>
[Back to top](#top)
<% }); //foreach sub  -%>
<% }); //foreach group -%>
