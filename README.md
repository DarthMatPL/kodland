import discord, random
from discord.ext import commands

intents = discord.Intents.default()
intents.message_content = True

bot = commands.Bot(command_prefix='!', intents=intents)

@bot.event
async def on_ready():
    print(f'Zalogowano jako{bot.user.name}')

@bot.command()
async def dodaj(ctx, a:int, b:int):
    await ctx.send(f'suma: {a + b}')

@bot.command()
async def odejm(ctx, a:int, b:int):
    await ctx.send(f'roznica: {a - b}')

@bot.command()
async def hej(ctx, count = 5):
    await ctx.send('hej' * count)



@bot.command()
async def password(ctx, lenn=10):
    symbols = 'qwertyuiop1234567890asdfghjklzxcvbnm'
    password=''
    for i in range(lenn):
        password += random.choice(symbols)
    await ctx.send(f'Wygenerowane haslo: {password}')


@bot.command()
async def repeat(ctx, times: int, content = 'powtorz'):
    for i in range(times):
        await ctx.send(content)

@bot.command()
async def moneta(ctx):
    a = random.randint(1,2)
    if a == 1:
        await ctx.send(f'Wypadła reszka')
    else:
        await ctx.send(f'Wypadł orzeł')

choices = ['kamien', 'papier', 'nozyce']
@bot.command()
async def rps(ctx, choice):
    user_choice = choice.lower()
    bot_choice = random.choice(choices)
    if user_choice not in choices:
        await ctx.send('niepoprawny wybor')
        return
    elif user_choice == bot_choice:
        await ctx.send(f'wybralem {bot_choice} remis...')
    elif (user_choice == 'kamien' and bot_choice == 'nozyce') or \
         (user_choice == 'papier' and bot_choice == 'kamien') or \
         (user_choice == 'nozyce' and bot_choice == 'papier'):
        await ctx.send(f'wygrales, wybralem {bot_choice}')
    else:
        await ctx.send(f'przegrales, wybralem {bot_choice}')


bot.run('MTI4NTYzNTI4NDQ2MDg5NjI4Ng.GC9TX0.RZphvqVfG1Hh92uvOc8uzT5cL227wdW1qZ0nns')
