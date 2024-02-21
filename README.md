import discord
from discord.ext import commands

# Initialise le bot
bot = commands.Bot(command_prefix='/')

# Événement lorsque le bot est prêt
@bot.event
async def on_ready():
    print(f'Connecté en tant que {bot.user.name}')

# Commande pour obtenir des informations sur un brawler
@bot.command()
async def brawler(ctx, nom):
    if nom.lower() == 'shelly':
        description = "Shelly est une brawler commune, armée d'un fusil à pompe. Elle peut infliger de gros dégâts à courte portée."
        image_url = "URL_DE_L_IMAGE_SHELLY"
    elif nom.lower() == 'colt':
        description = "Colt est un brawler rare, équipé de deux revolvers. Il excelle dans les combats à moyenne distance."
        image_url = "URL_DE_L_IMAGE_COLT"
    # Ajoutez d'autres brawlers avec leurs descriptions et images
    else:
        description = "Brawler non trouvé."
        image_url = ""
    
    embed = discord.Embed(title=nom.capitalize(), description=description, color=discord.Color.blue())
    if image_url:
        embed.set_thumbnail(url=image_url)
    await ctx.send(embed=embed)

# Commande pour obtenir des informations sur les modes de jeu
@bot.command()
async def mode(ctx, nom):
    if nom.lower() == 'bounty':
        description = "Bounty est un mode de jeu où l'équipe qui accumule le plus de points en éliminant les membres de l'équipe adverse remporte la partie."
    elif nom.lower() == 'gem grab':
        description = "Gem Grab est un mode de jeu où les équipes doivent collecter et conserver des gemmes tout en éliminant les adversaires pour gagner."
    # Ajoutez d'autres modes de jeu avec leurs descriptions
    else:
        description = "Mode de jeu non trouvé."
    
    embed = discord.Embed(title=nom.capitalize(), description=description, color=discord.Color.green())
    await ctx.send(embed=embed)

# Commande pour afficher les événements en cours
@bot.command()
async def evenements(ctx):
    evenements_embed = discord.Embed(title="Événements en cours", color=discord.Color.gold())
    evenements_embed.add_field(name="Événement 1", value="Description de l'événement 1", inline=False)
    evenements_embed.add_field(name="Événement 2", value="Description de l'événement 2", inline=False)
    # Ajoutez d'autres événements en cours
    await ctx.send(embed=evenements_embed)

# Commande pour déconnecter le bot
@bot.command()
async def deconnexion(ctx):
    await ctx.send("Déconnexion...")
    await bot.close()

# Lance le bot avec le token approprié
bot.run('TON_TOKEN_DISCORD')
