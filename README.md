import random
import discord
from discord.ext import commands
intents = discord.Intents.default()
intents.message_content = True
objetos = {
    "botella de plastico": "caneca blanca",
    "papel o carton": "caneca blanca",
    "vidrio": "caneca blanca",
    "metales": "caneca blanca",
    "papel higenico": "caneca negra",
    "servilletas": "caneca negra",
    "empaques sucios": "caneca negra",
    "comida": "caneca verde",
    "resciduos de jardineria": "caneca verde",
    "jeringas": "caneca roja",
    "medicamentos": "caneca roja",
    "quimicos": "caneca roja"
}
bot = commands.Bot(command_prefix='$', intents=intents)
@bot.event
async def on_ready():
    print(f'Hemos iniciado sesión como {bot.user}')

@bot.command()
async def clasificar(ctx, *, residuo: str):
    residuo_ej = residuo.lower()
    if residuo_ej in objetos:
        caneca = objetos[residuo_ej]
        await ctx.send(f"{residuo}** va en la **{caneca}**")
    else:
        await ctx.send(f"No conozco '{residuo}'. Intenta con otro residuo.")
@bot.command()
async def tipos(ctx):
    await ctx.send(f"los residuos identificados son: {', '.join(objetos.keys())}")

bot.run('token')
