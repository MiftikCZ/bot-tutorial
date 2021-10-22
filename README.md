# bot-tutorial
Tady najdete jak udělat discord bota

# Setup
```js
const miftcmd = require("@miftikcz/miftcmd")
const client = new miftcmd({
    prefix: "?", // sem si dej prefix
    status = "sem můžeš status discord bota, ALE nemusíš",
})


tady na tom místě budeš psát příkazy které uvidíš v dalších odstavcích


// pokud chceš před-udělaný help příkaz
client.use.pre_build_help()

// pokud chceš před-udělaný invite příkaz
client.use.pre_build_invite()

// tímhle řádkem přihlásíš bota
client.log(process.env.token)
```

# První příkaz
```js
// Jdeme udělat příkaz ?ahoj který odpoví "AHOJ!"
client.command("ahoj", {
  execute({message}) => {
    message.reply("AHOJ!", true) // true = žádný ping, false = s pingem
  }
})
```


# První static příkaz
```js
// Tohle funguje stejně jako client.command ale má to statickou odpověd
client.static("ahoj", "AHOJ!")
```


# První embed příkaz
```js
client.command("embed", {
  execute({message, Discord}) => {
    // uděláme embed
    const embed = new Discord.MessageEmbed()
    .setTitle("To co se zobrazí nahoře v embedu")
    .setDescription("řádek 1\nřádek 2\řádek 3...") /*do "" napiš uplně cokoliv*/
    
    // odešleme embed
    message.channel.send(embed)
    // pokud používáš embed tak nesmíš použít message.reply u příkazu!
  }
})
```


# příkaz který bude obsahovat aliases
```js
// aliases znamená, třeba: příkaz ahoj má alias "a", takže se může zpusit pomocí ?a příkazu
client.command("ahoj", {
  execute({message, command}) => {
    message.reply("funguje! použil jsi: " + command)
  },
  aliases: ["a"]
})
```
