# Arunika

The project name is Arunika. It is a talking doll project.

## Project Structures


```
. (project-root)
+- docs
|  +- prd         --> product requirement document
|  +- trd         --> technical requirement document
+- apps
   +- backend     --> code for backend
   +- device      --> code for device, currently esp32
```

## Tech Stack
- **Backend**: Go
- **Device (ESP32)**: C
- **Database**: scyllaDB
- **Communication**: WebSocket

## Key Conventions
- Branch naming: `<app>/<semantic-type>/<scope>`
- Commit style: `<semantic-type>: <message>`

## ScyllaDB

- Host: 127.0.0.1
- Port: 9042
- DB: arunika
- Username: arunika_usr
- Password: arunika_pwd
