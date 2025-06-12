# Telegram Bot MCP Server

This project is a **Telegram bot integration** built using the [Model Context Protocol (MCP)](https://modelcontextprotocol.org/) that exposes a suite of useful tools for interacting with the Telegram Bot API. It enables standardized communication with Telegram via a structured set of commands such as messaging, user management, and bot profile configuration.

> **Note:** This project is a fork of [siavashdelkhosh81/telegram-bot-mcp-server](https://github.com/siavashdelkhosh81/telegram-bot-mcp-server) with a few improvements:
>
> - Converted from TypeScript to pure JavaScript
> - Updated some of the tools

---

## Features

This MCP server exposes the following tools:

### Bot Information

- **get-me** - Test your bot's authentication and retrieve basic information about the bot

### Messaging

- **send-message** - Send a plain text message to a specific user or chat

  - `chatId`: Target chat ID or username (string, required)
  - `text`: Message content (string, required)
  - `replyToMessageId`: ID of the message to reply to (number, optional)
  - `parseMode`: Text markup mode - `Markdown`, `MarkdownV2`, or `HTML` (string, optional, default: `MarkdownV2`)

- **send-photo** - Send a photo with an optional caption
  - `chatId`: Target chat ID or username (string, required)
  - `media`: File ID, URL, or uploaded file (string, required)
  - `text`: Caption for the photo (string, optional)

### Chat Management

- **kick-chat-member** - Ban a user from a group, supergroup, or channel

  - `chatId`: Target chat (string, required)
  - `userId`: User to ban (number, required)

- **un-ban-chat-member** - Unban a previously banned user from a chat

  - `chatId`: Target chat (string, required)
  - `userId`: User to unban (number, required)

- **get-chat** - Fetch full chat metadata and details

  - `chatId`: Target chat (string, required)

- **get-chat-member-count** - Get the total number of members in a group or channel

  - `chatId`: Target chat (string, required)

- **get-chat-member** - Get detailed info about a specific member in a group or channel
  - `chatId`: Target chat (string, required)
  - `userId`: Target user (number, required)

### Bot Configuration

- **set-my-short-description** - Update your bot's short description (shown in the profile and shares)

  - `short_description`: New short description, max 120 characters (string, required)

- **get-my-short-description** - Fetch the current short description of the bot

- **set-my-commands** - Set the list of commands that appear in the Telegram UI

  - `commands`: Array of command objects with `{ command, description }` structure (array, required)

- **get-my-commands** - Get the current list of commands configured for the bot

- **set-my-name** - Update the name of the bot

  - `name`: New bot name (string, required)

- **get-my-name** - Retrieve the current name of the bot

- **set-my-description** - Update the full description of the bot (shown in empty chats)

  - `description`: New bot description, max 512 characters (string, required)

- **get-my-description** - Fetch the current description of the bot

## Installation

### 1. Get Your Telegram Bot Token

1. Open Telegram and search for [@BotFather](https://t.me/BotFather).
2. Start a conversation and run the command:
   ```
   /newbot
   ```
3. Follow the prompts to name your bot and get your **API token**.
4. Save the token.

### 2. Integration

You can use this MCP server directly without cloning by using npx:

```bash
npx -y telegram-bot-mcp
```

Then configure your MCP client with the following configuration:

```json
{
  "mcpServers": {
    "telegram_bot": {
      "command": "npx",
      "args": ["-y", "telegram-bot-mcp"],
      "env": {
        "TELEGRAM_BOT_API_TOKEN": "your bot token"
      }
    }
  }
}
```

## Development

If you want to contribute or run from source:

```bash
git clone https://github.com/imajus/telegram-bot-mcp-server.git
cd telegram-bot-mcp-server
```

Install packages:

```bash
npm install
```

Run the server in stdio mode:

```bash
npm start
```

For local testing, add this to your MCP client configuration:

```json
{
  "mcpServers": {
    "telegram_bot": {
      "command": "node",
      "args": ["/ABSOLUTE/PATH/TO/PARENT/FOLDER/index.js"],
      "env": {
        "TELEGRAM_BOT_API_TOKEN": "your bot token"
      }
    }
  }
}
```

Replace `/ABSOLUTE/PATH/TO/PARENT/FOLDER/index.js` with the real path to your project entry point.

## Support & Feedback

Feel free to open issues or contribute to the project. For Telegram-specific help, refer to the [Telegram Bot API documentation](https://core.telegram.org/bots/api).

Buy the [original author](https://github.com/siavashdelkhosh81) a Coffee: https://buymeacoffee.com/delkhoshsiv

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
