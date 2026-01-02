# Steam Game Recommender - Docker Guide 🐳

Pull and run the Steam Game Recommender using Docker.

## Quick Start

### 1. Get Your Steam Credentials

**Steam API Key:**

- Visit https://steamcommunity.com/dev/apikey
- Login with your Steam account
- Enter a domain name (can be `localhost` for personal use)
- Copy your API key

**Steam ID:**

- Visit https://steamid.io/ or https://www.steamidfinder.com/
- Enter your Steam profile URL or username
- Copy your Steam ID (64-bit/steamID64)

### 2. Pull and Run

**Using Docker directly:**

```bash
docker pull lquincarter/steam-game-recommender:latest

docker run -d \
  -p 3000:80 \
  -e STEAM_API_KEY=your_steam_api_key_here \
  -e STEAM_ID=your_steam_id_here \
  --name steam-recommender \
  lquincarter/steam-game-recommender:latest
```

**Using Docker Compose:**

Create a `docker compose.yml` file:

```yaml
services:
  steam-recommender:
    image: lquincarter/steam-game-recommender:latest
    ports:
      - "3000:80"
      - "3001:3001" # backend api
    restart: unless-stopped
    volumes:
      - ./data:/data
```

Then run:

```bash
docker compose up -d
```

### 3. Access the App

Open your browser and navigate to:

```
http://localhost:3000
```

## Available Tags

- `latest` - Latest stable release
- `v1.0.0` - Specific version tags

## Common Commands

```bash
# View logs
docker logs steam-recommender

# Stop the container
docker stop steam-recommender

# Start the container
docker start steam-recommender

# Remove the container
docker rm steam-recommender

# Pull latest version
docker pull lquincarter/steam-game-recommender:latest
```

## Updating

```bash
# Pull the latest image
docker pull lquincarter/steam-game-recommender:latest

# Restart with docker compose
docker compose down
docker compose up -d

# Or restart the container directly
docker stop steam-recommender
docker rm steam-recommender
docker run -d \
  -p 3000:80 \
  -e STEAM_API_KEY=your_key \
  -e STEAM_ID=your_id \
  --name steam-recommender \
  lquincarter/steam-game-recommender:latest
```

## Troubleshooting

**Container won't start:**

- Ensure port 3000 is not already in use: `lsof -i :3000`
- Check logs: `docker logs steam-recommender`

**API errors:**

- Verify your Steam API key is valid
- Ensure your Steam ID is in 64-bit format (17 digits)
- Check that your Steam profile is public

**No recommendations showing:**

- Make sure you have played some games in your Steam library
- Try refreshing the data using the refresh button in the app

## Support

For issues or questions, visit: https://github.com/quincarter/steam-game-recommender/issues
