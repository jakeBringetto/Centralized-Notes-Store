---
description: Setting up an o3 instance
---

# Frontend Setup

### Docker Version:

1. Clone the [distro-config(opens in a new tab)](https://github.com/openmrs/openmrs-distro-referenceapplication) repository.
2. Launch Docker Desktop
3. Run `docker compose build` from the root of the repository (You might need to run `docker-compose build` instead if you're using `docker-compose`).
4. Once the build completes, run `docker compose up` (or `docker-compose up` if you're using `docker-compose`).
5. You should be able to launch O3 by visiting `http://localhost/openmrs/spa` in your browser.
