---
title: Dependency Management
parent: Reproducibility
---

# Dependency Management

Dependency management tools help create reproducible environments by tracking and managing package dependencies. This generally comes in some form of 'lockfile' that records or enforces the specific versions of packages used for a project. 

## General Best Practices

1. **Document Dependencies**: Explain why each package is needed
2. **Version Control**: Track dependency files in version control
3. **Regular Updates**: Keep dependencies up-to-date
4. **Environment Isolation**: Use project-specific environments
5. **Testing**: Verify environment recreation works

## R: renv

renv is the standard dependency management tool for R projects.

## Python: UV

UV is a fast Python package installer and resolver, designed to be a drop-in replacement for pip and pip-tools.

## Resources

### R
- [renv Documentation](https://rstudio.github.io/renv/)

### Python
- [UV Documentation](https://github.com/astral-sh/uv)
