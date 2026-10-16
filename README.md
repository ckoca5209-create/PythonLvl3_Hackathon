# PythonLvl3_Hackathon
python lvl 3 için yazdığım heckhaton
import os

import discord
from discord.ext import commands

intents = discord.Intents.default()
intents.message_content = True 

bot = commands.Bot(command_prefix='!', intents=intents)


fikir_katalogu = {
    "pet şişe": [
        "Altını kesip boyayla boyayarak şirin bir saksı yapabilirsin.",
        "Ortasını delip içine tahta kaşıklar sokarak kuş yemliğine dönüştürebilirsin."

    ],
    "karton": [
        "Kablolarını düzenlemek için bölmeli bir kutu yapabilirsin.",
        "Maket bıçağıyla keserek benim gibi çalışmayan süs bir gitar yapabilirsin."
    ],
    "eski tişört": [
        "Alt kısmını kesip bağlayarak dikişsiz bir bez çanta yapabilirsin.",
        "benim yaptığım gibi eski bir tişörtü makas ile maske yapabilirsin"
    ]
}
@bot.event
async def on_ready():
    print(f' giriş yapıldı   Geri dönüşüm fikirleri vermeye hazır.')


@bot.event
async def on_message(message):
    
    if message.author == bot.user:
        return   
    mesaj_icerigi = message.content.lower()
    
    bulunan_fikirler = []
    
    
    for malzeme, fikirler in fikir_katalogu.items():
        if malzeme in mesaj_icerigi:
            bulunan_fikirler.append((malzeme, fikirler))
            
    # Eğer cümlede bir malzeme bulduysak, cevap hazırlayıp gönderelim
    if bulunan_fikirler:
        cevap = f"Selam {message.author.mention}! O malzemeyle harika şeyler yapabilirsin:\n"
        
        for malzeme, fikirler in bulunan_fikirler:
            cevap += f"\n **{malzeme.upper()} İÇİN FİKİRLER:**\n"
            for i, fikir in enumerate(fikirler, 1):
                cevap += f"{i}. {fikir}\n"
                
        await message.channel.send(cevap)

    
    await bot.process_commands(message)



bot.run("MTQ2MTc4NDQ2ODg3NTM3ODkzMg.GbimxQ.infP1dCzbjDkrTLF2YABu01AmDK6CrcLceX5ts")

