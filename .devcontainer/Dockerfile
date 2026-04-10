FROM mcr.microsoft.com/devcontainers/python:1-3.12-bullseye 
# Use any image suitable for your project

WORKDIR /home/vscode/workspace
# Initiate package manager
RUN sudo rm -f /etc/apt/sources.list.d/yarn.list
RUN sudo apt update
# opencode
RUN sudo apt install nodejs npm -y
RUN npm i -g opencode-ai@1.4.3
