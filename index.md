---
slug: github-document-parser
title: 'Document-Parser: FastAPI API for Multi-Format Document Ingestion and Parsing'
repo: justin-napolitano/document-parser
githubUrl: https://github.com/justin-napolitano/document-parser
generatedAt: '2025-11-23T08:52:19.498640Z'
source: github-auto
summary: >-
  Technical overview of a document parsing API built with FastAPI and Unstructured library
  supporting PDFs, Word, HTML, images, and gzip files.
tags:
  - document-parsing
  - fastapi
  - unstructured
  - pdf
  - api
  - docker
seoPrimaryKeyword: document parsing
seoSecondaryKeywords:
  - fastapi api
  - unstructured library
  - multi-format documents
seoOptimized: true
---

# document-parser: Technical Overview and Implementation

## Motivation and Problem Statement

The document-parser project addresses the challenge of processing and extracting structured information from heterogeneous document formats. Many organizations require automated pipelines to ingest documents such as PDFs, Word files, emails, HTML pages, and images, then parse and tokenize the content for storage, analysis, or further processing. Existing tools often lack flexibility, extensibility, or comprehensive support for diverse file types.

This project leverages the Unstructured library to provide a robust parsing backend and builds an API layer to facilitate document partitioning, chunking, and extraction of entities, relationships, and citations. It aims to standardize document ingestion into a database-ready format.

## Architecture and Components

### Core Parsing Engine

The core of the system is built on the Unstructured library, which provides document partitioning capabilities. It supports multiple file types and can detect file types automatically. The project wraps this functionality in a FastAPI-based REST API, exposing endpoints for document submission and retrieval of parsed elements.

### API Layer

The API is implemented with FastAPI, offering:

- Multipart file upload support
- Form parameters for controlling parsing behavior (e.g., chunking strategy, OCR languages, output format)
- Content type validation and detection, including handling of gzip compressed files
- Custom OpenAPI schema generation with API key security scheme (though full implementation is pending)
- Exception handling for HTTP errors and generic exceptions with consistent JSON responses

### Document Processing

Documents are processed in multiple stages:

- File type detection using the Unstructured library's detection utilities
- Validation of partitionable file types
- Optional decompression for gzip files
- Partitioning into elements using Unstructured's partition function
- Conversion to various output formats such as JSON or CSV
- Support for chunking and multipage sectioning to handle large documents

### Utilities and Helpers

The project includes utilities for:

- Smart parsing of form parameters to handle different input formats (e.g., strings, lists, booleans)
- Logging configuration tailored for API and inference components
- PDF manipulation using pypdf for splitting and handling encrypted files
- File type validation and mimetype normalization

### Deployment and Testing

A Docker Compose configuration is provided to run the Unstructured service container, which the API depends on. The API itself can be run with Uvicorn. The project includes a comprehensive test suite using pytest that covers API endpoints, gzip handling, and utility functions.

## Implementation Details

- The API router is modularized, with a `general` router handling the main document parsing endpoint.
- Form parameters are modeled with Pydantic, supporting validation and conversion via custom validators.
- The OpenAPI schema is customized to include retry strategies and security schemes.
- Logging is configured to separate access and error logs, with environment-based disabling of verbose logs.
- The system supports a beta "Chipper" model for high-resolution document processing, indicating extensibility for inference models.
- The API can handle multiple files in a single request, including mixed compressed and uncompressed inputs.

## Practical Considerations

- File type detection is robust, falling back to content inspection if headers are unreliable.
- The API design anticipates future authentication via API keys.
- Chunking strategies and parameters allow fine-tuning for different document sizes and types.
- The project includes sample documents and smoketests to validate end-to-end functionality.

## Summary

This project provides a practical and extensible solution for document parsing pipelines, combining a powerful parsing library with a clean API interface. Its modular design and comprehensive utilities facilitate integration into larger data processing workflows. The use of FastAPI and Docker ensures easy deployment and scalability. Future enhancements will likely focus on improving parsing accuracy, expanding supported formats, and adding security and operational features.

