# Local OpenCode Setup Guide

## Overview
This guide explains how to set up and run OpenCode locally using LMStudio.

## Prerequisites
This setup is using Docker Desktop. If you are using a setup without Docker Desktop, add `network_mode: "host"` to your `.devcontainer/docker-compose.yml` file and adjust the server address in `opencode.json` accordingly to `localhost`.

## Setup Steps

### 1. Install and Configure LMStudio
- Download and install [LMStudio](https://lmstudio.ai/)
- Launch the application

### 2. Load the Model
- Open LMStudio
- Navigate to the Models section
- Search for and download the model referenced in your `opencode.json` file (here it is `openai/gpt-oss-20b`)
- Wait for the download to complete

### 3. Configure Context Window
- In LMStudio `Developer` Tab select the model, and adjust the context window settings. Set the context window to the **maximum allowed value** for your selected model (OpenCode nneds a large Context)

### 4. Start the Web Server
- In LMStudio, go to the `Developer` tab > `Local Server`
- In the top left there is a toggle to start the server, click it to start the server.
- The server will typically run on `http://localhost:1234` (or the port shown in LMStudio)
- Verify the server is running and accessible (e.g. using `curl http://localhost:1234/v1 -vv`. You are looking for a successful connection, not for a valid response)
Successful connection snippet: 
```
...

* Connected to localhost (127.0.0.1) port 1234
> GET /v1 HTTP/1.1
> Host: localhost:1234
> User-Agent: curl/8.7.1
> Accept: */*
> 
* Request completely sent off
< HTTP/1.1 200 OK

...
```
### 5. Connect OpenCode
- Open this VsCode workspace as a Dev Container (if not already in a Dev Container)
- In the `opencode.json` you see the adress `http://host.docker.internal:1234/v1`. This Adress works when running with Docker Desktop. 
- If you are running without Docker Desktop, change the adress to `http://localhost:1234/v1`, and add `network_mode: "host"` to your `.devcontainer/docker-compose.yml` file, and rebuild the container.


### 6. Test the Connection
- Open a terminal and run `opencode`
- Write `test` or whatever. You should see a response from the model, confirming that OpenCode is successfully connected to the LMStudio server.
- When the response takes alot of time, have a look in LMStudio. Here you can see the logs of the LM Server. There should be a log entry like `[openai/gpt-oss-20b] Prompt processing progress: 20.7%`

## Privacy and Data Handling
**This is my personal understanding of the matter** 
This is not a legal advice, or contract. You have to verify these statements on your own. 

- OpenCode processes your code and data locally on your machine. It does not send your code or data to any external servers.
- The connection between OpenCode and LMStudio is local, ensuring that your code and data remain private and secure on your machine.
- In the Privacy statement of OpenCode, they state, that they will collect telemtry data. **I do not know what this means for local operation** 
- If you have concerns about data privacy, review the OpenCode privacy policy and consider reaching out to the OpenCode team for clarification on data handling practices in local setups.

## Notes
- Ensure sufficient system resources (RAM, GPU) for smooth operation
- Keep LMStudio running while using OpenCode locally
