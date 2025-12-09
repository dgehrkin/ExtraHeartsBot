# ExtraHeartsBot

A Discord bot designed to manage the Extra Hearts guild on Hypixel. This bot tracks guild credits, monitors member activity, and provides useful commands for guild management.

## Features

- **Guild Credit System**: Automatically awards credits to the top 10 daily GEXP earners
- **Member Tracking**: Monitors guild member joins and leaves, sending notifications to Discord
- **Leaderboard**: View guild credits leaderboard with pagination support
- **Member Information**: Look up detailed information about guild members
- **Credit Management**: Admin commands to add, subtract, or set member credits
- **Automated Daily Rewards**: Distributes credits daily at 23:15 based on GEXP earned

## Prerequisites

- Node.js (v16 or higher recommended)
- A Discord Bot Token
- A Hypixel API Key
- Discord Bot with appropriate permissions

## Installation

1. Clone the repository:
```bash
git clone https://github.com/dgehrking/ExtraHeartsBot.git
cd ExtraHeartsBot
```

2. Install dependencies:
```bash
npm install
```

3. Create a `.env` file in the root directory with the following variables:
```env
BOT_TOKEN=your_discord_bot_token
API_KEY=your_hypixel_api_key
CLIENT_ID=your_discord_client_id
GUILD_ID=your_discord_guild_id
```

4. Deploy Discord slash commands:
```bash
node deploy-commands.js
```

5. Start the bot:
```bash
node index.js
```

## Commands

### User Commands

- `/help` - Displays a list of available commands
- `/info` - Shows general information about the bot
- `/lb [username]` - Displays the guild credits leaderboard (optionally jump to a specific member)
- `/member <username>` - Shows detailed information about a guild member

### Admin Commands

- `/addcredits <username> <amount>` - Add credits to a member
- `/subtractcredits <username> <amount>` - Subtract credits from a member
- `/setcredits <username> <amount>` - Set a member's credits to a specific amount
- `/remove <username>` - Remove a member from the database
- `/removeinactive` - Remove inactive members from the database
- `/filldata` - Fill database with missing guild member data

## How It Works

### Credit System

The bot automatically calculates and awards credits based on daily GEXP (Guild Experience):
- Credits are calculated as: `Math.floor(dailyGexp / 10000)`
- Only the top 10 daily GEXP earners receive credits
- Credits are distributed daily at 23:15 (11:15 PM)

### Member Tracking

- The bot checks the guild roster every minute
- When new members join, they are automatically added to the database
- Join/leave notifications are sent to a designated Discord channel
- Member data includes UUID, IGN (In-Game Name), and credits

### Database

The bot uses SQLite with Sequelize ORM to store:
- Member UUIDs
- In-Game Names (IGN)
- Credit balances
- Guild ranks

## Project Structure

```
ExtraHeartsBot/
├── commands/          # Discord slash command files
│   ├── addcredits.js
│   ├── filldata.js
│   ├── help.js
│   ├── info.js
│   ├── lb.js
│   ├── member.js
│   ├── remove.js
│   ├── removeinactive.js
│   ├── setcredits.js
│   └── subtractcredits.js
├── models/            # Sequelize database models
│   └── credits.js
├── utils/             # Utility functions
│   └── database.js
├── deploy-commands.js # Command deployment script
├── index.js           # Main bot file
└── package.json       # Dependencies and project info
```

## Dependencies

- `discord.js` ^14.25.1 - Discord API wrapper
- `hypixel-api-reborn` ^12.0.0-17 - Hypixel API client
- `sequelize` ^6.32.0 - SQL ORM
- `sqlite3` ^5.1.6 - SQLite database driver
- `dotenv` ^17.2.3 - Environment variable management
- `node-fetch` ^2.6.7 - HTTP requests

## Configuration

### Required Environment Variables

- `BOT_TOKEN`: Your Discord bot token
- `API_KEY`: Your Hypixel API key
- `CLIENT_ID`: Your Discord application client ID
- `GUILD_ID`: Your Discord server (guild) ID

### Channel IDs

The bot uses hardcoded channel IDs for notifications. You may need to update these in `index.js`:
- Line 99: Credits notification channel
- Line 179: Member join/leave notification channel

## Contributing

This is a work in progress. Suggestions and contributions are welcome! If you have ideas or find bugs, please open an issue.

## License

ISC

## Author

**IdkDom**

- GitHub: [@dgehrking](https://github.com/dgehrkin)

## Links

- [Extra Hearts Guild Website](https://extraheartsguild.webnode.com/)
- [Repository](https://github.com/dgehrkin/ExtraHeartsBot)
- [Issues](https://github.com/dgehrkin/ExtraHeartsBot/issues)

## Notes

- The bot requires appropriate Discord permissions (Send Messages, Embed Links, etc.)
- Make sure your Hypixel API key has access to guild data
- The bot runs continuously and checks the guild every minute
- Database file (`database.sqlite`) will be created automatically on first run

