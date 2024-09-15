---
title: |
  News
menu:
  main:
    weight: 20
weight: 20
bookCollapseSection: true
---

# What's happened lately in the fluxbox world?

Find announces in here, updates, statements and so on.

{{ range .Paginator.Pages }}
  <h2><a href="{{ .RelPermalink }}">{{ .LinkTitle }}</a></h2>
{{ end }}

{{ template "_internal/pagination.html" . }}
