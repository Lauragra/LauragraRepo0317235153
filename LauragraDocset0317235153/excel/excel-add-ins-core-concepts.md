# Core concepts

## JavaScript APIs

* common APIs versus shared APIs
* office versions
* requirement sets -- what they are, why they matter, checking for supportability in JS code
* open specifications page

## Manifest

describe what manifest controls -- include details (and links out to relevant content) for: 

* define add-in commands 
* specify office hosts
* specify permissions
* ...

## Lifecycle of an add-in

> See: https://dev.office.com/docs/add-ins/develop/add-in-development-lifecycle

### Design

* design and implement the UI/UX
* link to: [Design your Office Add-ins](../design/add-in-design.md?product=excel)

### Develop 

* ...

### Test and debug

Test:
* sideloading an add-in for testing (3 ways?)

Debug:
* attach debugger from task pane
* debug (3 ways)
* validate and troubleshoot issues with your manifest

### Publish

* publish web app:  host on Azure or elsewhere
* publish manifest: via centralized deployment | to add-in catalog | to the Office Store (include link to validation policies)

### Maintain

* ...