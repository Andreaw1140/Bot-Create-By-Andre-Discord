Langkah 1: Siapin Peralatan
Pastikan lo punya Node.js di komputer lo, ya. Lo bisa download dari situs resmi Node.js, bro.

Langkah 2: Inisialisasi Proyek Node.js
Buka terminal atau command prompt, terus buat folder baru buat proyek lo. Masuk ke folder itu dan jalankan perintah ini:

bash
Copy code
npm init -y
Langkah 3: Instal Pustaka-pustaka yang Diperlukan
Di terminal, lo harus install pustaka Discord.js, @discordjs/voice, dan ytdl-core. Cukup jalankan perintah berikut:

bash
Copy code
npm install discord.js @discordjs/voice ytdl-core
Langkah 4: Bikin Bot Discord
Buat file baru namanya bot.js. File JavaScript ini bakal jadi tempat lo tulis kode buat bot Discord lo.

Langkah 5: Salin dan Tempel Kode
Salin kode berikut dan tempel ke dalam file bot.js:

javascript
Copy code
const { Client, Intents } = require('discord.js');
const { joinVoiceChannel, createAudioPlayer, createAudioResource, StreamType, AudioPlayerStatus } = require('@discordjs/voice');
const ytdl = require('ytdl-core');

const client = new Client({ intents: [Intents.FLAGS.GUILDS, Intents.FLAGS.GUILD_VOICE_STATES] });
const player = createAudioPlayer();

client.once('ready', () => {
    console.log('Bot udah siap, bro!');
});

client.on('messageCreate', async message => {
    if (!message.guild) return;
    if (message.content.startsWith('!main')) {
        const voiceChannel = message.member.voice.channel;
        if (!voiceChannel) return message.reply('Masuk voice channel dulu, bre!');

        const connection = joinVoiceChannel({
            channelId: voiceChannel.id,
            guildId: voiceChannel.guild.id,
            adapterCreator: voiceChannel.guild.voiceAdapterCreator
        });

        const url = message.content.split(' ')[1];
        if (!url) return message.reply('Masukin link lagu, nih!');

        const stream = ytdl(url, { filter: 'audioonly' });
        const resource = createAudioResource(stream, { inputType: StreamType.Arbitrary });

        connection.subscribe(player);
        player.play(resource);
        message.reply('Nih, aku mainin lagunya, bre!');
    }
});

client.login('TOKEN_BOT_KAMU');
Jangan lupa ganti 'TOKEN_BOT_KAMU' dengan token bot Discord lo.

Langkah 6: Jalankan Bot
Di terminal, ketik perintah ini buat jalankan bot lo:

bash
Copy code
node bot.js
Langkah 7: Coba Bot
Buka Discord, undang bot ke server lo. Terus, coba kirim pesan !main [LINK_YOUTUBE] di salah satu saluran teks buat mainin lagu dari YouTube.
