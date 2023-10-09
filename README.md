# mydcpj0
import discord
import random
import asyncio
# Variabel intents menyimpan hak istimewa bot
intents = discord.Intents.default()
# Mengaktifkan hak istimewa message-reading
intents.message_content = True
# Membuat bot di variabel klien dan mentransfernya hak istimewa
client = discord.Client(intents=intents)

@client.event
async def on_ready():
    print(f'Kita telah masuk sebagai {client.user}')

@client.event
async def on_message(message):
    if message.author == client.user:
        return
    if message.content.startswith('$halo'):
        await message.channel.send("Hi!")
    elif message.content.startswith('$bye'):
        await message.channel.send("\\U0001f642")
        handler = random.choise (1, 3)
        if handler ==1:
            await message.channel.send("Good by bro")
        elif handler == 2:
            await message.channel.send("Good job")
        elif handler == 3:
            await message.channel.send("Welcome")
    elif message.content.startswith('$deleteme'):
        msg = await message.channel.send('I will delete myself now...')
        await msg.delete()
    elif  message.content.startswith('$hello'):
            await message.reply('Hello!', mention_author=True)
    else:
        await message.channel.send(message.content)
@client.event
async def on_message_delete(message):
     msg = f'{message.author} has deleted the message: {message.content}'
     await message.channel.send(msg)
@client.event
async def on_message(client, message):
    if message.author.id == client.user.id:
        return
@client.event.user.id
async def on_ready():
    print(f'Logged in as {client.user} (ID: {client.id})')
    print('------')

async def on_message(message):
        
    if message.author.id == client.user.id:
            return

    if message.content.startswith('$guess'):
        await message.channel.send('Guess a number between 1 and 10.')

        def is_correct(m):
            return m.author == message.author and m.content.isdigit()

            answer = random.randint(1, 10)

            try:
                guess = await self.wait_for('message', check=is_correct, timeout=5.0)
            except asyncio.TimeoutError:
                return await message.channel.send(f'Sorry, you took too long it was {answer}.')

            if int(guess.content) == answer:
                await message.channel.send('You are right!')
            else:
                await message.channel.send(f'Oops. It is actually {answer}.')


