---
name: quantum-guppy-selene
description: Enables OpenClaw agents to build, deploy, and manage quantum computing applications using Quantinuum's Guppy/Selene stack with Fly.io backend hosting and Lovable frontend. Use when creating quantum-powered web applications, deploying quantum algorithms to the cloud, or integrating quantum computing results into user-facing interfaces.
---

# Quantum Guppy Selene Integration

## Overview

This skill provides everything needed to create production-ready quantum computing applications using Quantinuum's Guppy (quantum programming language) and Selene (backend service) stack. It automates deployment to Fly.io and frontend integration with Lovable, enabling agents to deliver complete quantum web applications without manual infrastructure setup.

## Core Capabilities

### 1. Create Full-Stack Quantum Applications
Generate complete quantum applications with Guppy algorithms, Selene backend API, and Lovable frontend in minutes.

### 2. Fly.io Deployment Automation
Automatically deploy Selene backend services to Fly.io with proper configuration, scaling, and domain setup.

### 3. Lovable Frontend Integration
Create frontend interfaces that connect to quantum backend APIs with real-time results visualization.

### 4. Quantum Algorithm Templates
Access pre-built quantum algorithms (optimization, chemistry, machine learning) as starting points.

### 5. Environment Configuration Management
Handle API keys, quantum hardware credentials, and Fly.io secrets securely.

## When to Use This Skill

**Trigger this skill when agents need to:**
- Build web applications that use quantum computing
- Deploy quantum algorithms as REST APIs
- Create dashboards for quantum computation results
- Set up quantum computing infrastructure quickly
- Integrate Guppy/Selene with modern frontend frameworks
- Prototype quantum solutions with production-ready deployment

**Example user requests:**
- "Build a quantum portfolio optimizer with a web interface"
- "Deploy my Guppy algorithm to the cloud with an API"
- "Create a Lovable frontend that visualizes quantum chemistry results"
- "Set up a quantum machine learning service on Fly.io"
- "Make a quantum random number generator web app"

## Workflow: Creating a Quantum Application

### Step 1: Define the Quantum Use Case
Identify the quantum computing problem (optimization, simulation, ML, cryptography, etc.)

### Step 2: Generate Guppy Algorithm
Write the quantum circuit using Guppy language. See `references/guppy_guide.md` for syntax.

### Step 3: Create Selene Backend
Wrap the Guppy algorithm in a Selene service with REST endpoints. Use `scripts/setup_selene_service.py` to scaffold.

### Step 4: Configure Fly.io
Set up Fly.io configuration. Use `scripts/flyio_deploy.py` to handle platform setup, build, and launch.

### Step 5: Build Lovable Frontend
Create a Lovable project that consumes the Selene API. Use `assets/lovable-template/` as a starting point.

### Step 6: Deploy and Connect
Deploy backend to Fly.io, then configure frontend environment variables to point to the live API.

## Quick Start Example

**User request:** "Create a quantum coin flip simulator with a web interface"

**Agent workflow:**
1. Use Guppy to create quantum superposition circuit (see `references/guppy_guide.md`)
2. Use `scripts/setup_selene_service.py` to scaffold backend with endpoint `/api/coin-flip`
3. Use `scripts/flyio_deploy.py` to deploy backend to Fly.io (get URL like `quantum-coins.fly.dev`)
4. Use `assets/lovable-template/` to create frontend with button triggering API
5. Connect frontend to backend URL and test

Result: Complete web app where users click a button to get quantum-random heads/tails.

## Resources (optional)

### scripts/
**Purpose:** Executable scripts that automate setup, deployment, and integration tasks.

#### Key Scripts:

- `setup_selene_service.py` - Scaffold a new Selene backend service with API endpoints for quantum algorithms
- `flyio_deploy.py` - Deploy Selene service to Fly.io, handling configuration, build, and launch
- `lovable_integrate.py` - Set up Lovable frontend project configured to connect to quantum backend
- `create_quantum_app.py` - All-in-one script that runs the full workflow end-to-end

#### Usage:
Scripts can be executed directly by Codex or imported as modules for programmatic access.

```bash
# Example: Create full application stack
python3 scripts/create_quantum_app.py --app-name "quantum-optimizer" --use-case "portfolio-optimization"
```

### references/
**Purpose:** Detailed documentation for Guppy language, Selene framework, and integration patterns.

#### Key Documents:

- `guppy_guide.md` - Complete Guppy programming reference: syntax, quantum gates, circuit construction, examples
- `selene_api.md` - Selene service architecture, endpoint definitions, request/response schemas, error handling
- `flyio_config.md` - Fly.io configuration for quantum workloads: scaling, regions, secrets, monitoring
- `lovable_patterns.md` - Frontend patterns for quantum apps: real-time visualization, results display, error states
- `deployment_checklist.md` - Step-by-step checklist for production deployment
- `security_best_practices.md` - Securing quantum API keys, rate limiting, authentication

#### Usage:
Read these files when implementing specific aspects of the quantum stack. They provide detailed API specifications and best practices.

### assets/
**Purpose:** Template files and boilerplate for rapid project creation.

#### Key Assets:

- `selene-template/` - Boilerplate Selene service with sample Guppy integration and Dockerfile
- `lovable-template/` - Lovable project pre-configured with quantum API client and visualization components
- `dockerfiles/` - Optimized Docker configurations for Guppy runtime, Selene service, and multi-stage builds
- `turborepo-config/` - Monorepo configuration for managing backend + frontend together

#### Usage:
Copy template directories as starting points for new projects. Modify configuration files based on quantum use case.

## Advanced: Multi-Quantum Use Cases

### Real-Time Quantum Optimization Dashboard
- Backend: Selene service running quantum optimization algorithms (QAOA, VQE)
- Frontend: Lovable dashboard with sliders for parameters, real-time result visualization
- Deploy: Fly.io with horizontal scaling for concurrent computations

### Quantum Chemistry Explorer
- Backend: Guppy simulations of molecular structures, energy calculations
- Frontend: 3D molecule viewer with computed properties, interactive parameter adjustment
- Deploy: Fly.io with persistent storage for simulation results

### Quantum Machine Learning API
- Backend: Selene service exposing quantum ML models (QNN, QSVM)
- Frontend: Lovable interface for uploading training data, running predictions, comparing classical vs quantum results
- Deploy: Fly.io with GPU acceleration if needed for hybrid classical-quantum processing

## Performance Considerations

- **Quantum job queuing**: Selene services should implement job queues for long-running quantum computations
- **Result caching**: Cache frequent identical computations to reduce quantum hardware costs
- **Fly.io scaling**: Configure appropriate VM sizes based on quantum hardware requirements (some Guppy operations need more memory)
- **Frontend responsiveness**: Use WebSockets or polling for long-running quantum jobs; provide progress indicators

## Cost Management

- Quantinuum quantum hardware usage incurs costs. Implement usage tracking and quotas in Selene layer
- Consider hybrid classical-quantum approaches to minimize expensive quantum circuit calls
- Cache results aggressively; quantum computations are expensive and often repeatable
- Fly.io costs scale with usage; configure autoscaling appropriately

## Security

- Never expose quantum hardware API keys in frontend. All quantum access must go through Selene backend
- Use Fly.io secrets management for credentials
- Implement rate limiting on Selene endpoints to prevent quantum resource exhaustion
- Add authentication/authorization for production apps (see `references/security_best_practices.md`)

## Troubleshooting

**Guppy compilation errors**: Check Guppy syntax against `references/guppy_guide.md`. Ensure all quantum gates are properly defined.

**Selene service not starting**: Verify Fly.io configuration in `fly.toml`. Check logs with `fly logs`. Ensure all environment variables are set.

**Frontend cannot connect**: Confirm CORS is enabled in Selene service. Check that Fly.io URL is correct and app is deployed. Verify API endpoint paths match.

**Quantum results incorrect**: Validate Guppy algorithm logic. Check for proper measurement and sampling. Review reference implementations in `assets/selene-template/examples/`.

## Next Steps

After initial setup:
1. Monitor quantum hardware usage and costs via Quantinuum dashboard
2. Add authentication to Selene API if exposing publicly
3. Implement comprehensive error handling and user feedback in frontend
4. Set up logging and monitoring on Fly.io
5. Consider adding database persistence for job history and results

---

**Not every skill requires all three types of resources.**
