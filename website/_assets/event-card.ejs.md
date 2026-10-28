<%
// Listing template for event cards (used by home.qmd and projects/overview.qmd).
// Each item is an event page: website/projects/<YYYY-MM-DD-name>/index.qmd
%>

::: {.card-grid}

<% for (const item of items) { %>

```{=html}
<a href="<%- item.path %>" class="photon-card event-card" <%= metadataAttrs(item) %>>
<% if (item.image) { %>
<img src="<%- item.image %>" alt="<%= item['image-alt'] || item.title %>" loading="lazy">
<% } %>
<span class="date"><%= item['date-display'] || item.date %></span>
<h4><%= item.title %></h4>
<% if (item.description) { %><p><%= item.description %></p><% } %>
<% if (item.venue) { %><span class="venue"><i class="bi bi-geo-alt"></i> <%= item.venue %></span><% } %>
</a>
```

<% } %>

:::
