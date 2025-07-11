FROM python:3.11-slim

WORKDIR /app

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git \
    curl \
    nginx \
    && rm -rf /var/lib/apt/lists/*
# Add nginx configuration
COPY ./docker/graphiti/nginx.conf /etc/nginx/nginx.conf

# Clone the Graphiti repository
RUN git clone https://github.com/getzep/graphiti.git .

# Navigate to MCP server directory and install dependencies
WORKDIR /app/mcp_server

# Install UV package manager
RUN pip install uv

# Sync dependencies
RUN uv sync

# Environment variables are handled by Docker Compose


# Expose ports
EXPOSE 8000
EXPOSE 8001

# Start nginx as a daemon and run the MCP server
CMD ["sh", "-c", "nginx && uv run graphiti_mcp_server.py --host 0.0.0.0"]