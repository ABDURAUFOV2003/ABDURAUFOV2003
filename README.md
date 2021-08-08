 aiogramLogo
latest
Search docs
Installation Guide
Quick start
Simple template
Summary
Migration FAQ (1.4 -> 2.0)
Telegram
Dispatcher
Utils
Examples
Contribution
Links
aiogram
Docs » Quick start
Quick start
Simple template
At first you have to import all necessary modules

import logging

from aiogram import Bot, Dispatcher, executor, types
Then you have to initialize bot and dispatcher instances. Bot token you can get from @BotFather

API_TOKEN = '1887076346:AAHT91OhQXOs6scH0uSUARTwmDQnUoFlP9k'

# Configure logging
logging.basicConfig(level=logging.INFO)

# Initialize bot and dispatcher
bot = Bot(token=API_TOKEN)
dp = Dispatcher(bot)
Next step: interaction with bots starts with one command. Register your first command handler:

@dp.message_handler(commands=['start', 'help'])
async def send_welcome(message: types.Message):
    """
    This handler will be called when user sends `/start` or `/help` command
    """
    await message.reply("Hi!\nI'm EchoBot!\nPowered by aiogram.")
If you want to handle all text messages in the chat simply add handler without filters:

@dp.message_handler()
async def echo(message: types.Message):
    # old style:
    # await bot.send_message(message.chat.id, message.text)

    await message.answer(message.text)
Last step: run long polling.

if __name__ == '__main__':
    executor.start_polling(dp, skip_updates=True)
Summary
 1"""
 2This is a echo bot.
 3It echoes any incoming text messages.
 4"""
 5
 6import logging
 7
 8from aiogram import Bot, Dispatcher, executor, types
 9
10API_TOKEN = 'BOT TOKEN HERE'
11
12# Configure logging
13logging.basicConfig(level=logging.INFO)
14
15# Initialize bot and dispatcher
16bot = Bot(token=API_TOKEN)
17dp = Dispatcher(bot)
18
19
20@dp.message_handler(commands=['start', 'help'])
21async def send_welcome(message: types.Message):
22    """
23    This handler will be called when user sends `/start` or `/help` command
24    """
25    await message.reply("Hi!\nI'm EchoBot!\nPowered by aiogram.")
26
27
28
29@dp.message_handler()
30async def echo(message: types.Message):
31    # old style:
32    # await bot.send_message(message.chat.id, message.text)
33
34    await message.answer(message.text)
35
36
37if __name__ == '__main__':
38    executor.start_polling(dp, skip_updates=True)
