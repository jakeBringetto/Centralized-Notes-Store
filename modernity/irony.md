---
description: Make a cool lyric call it the Meta - verse
---

# Irony

```javascript
else if (args[1].toLowerCase() === 'mock') {
        message.channel.messages.fetch({limit: 3})
        .then(messageMappings => {
        let messages = Array.from(messageMappings.values());
        let previousMessage = messages[1].content;
        for (var j = 0; j <=previousMessage.length / 3; ++j){
            var word_index = Math.floor(Math.random() * previousMessage.length);
            previousMessage = previousMessage.substring(0, word_index) + 
            previousMessage[word_index].toUpperCase() + 
            previousMessage.substring(word_index + 1);
        }
        message.channel.send(previousMessage.slice(0, 1999));
        })
        .catch(error => console.log(error))
```

{% embed url="https://www.youtube.com/watch?index=22&list=WL&v=nsuSveDAlpI" %}
cool
{% endembed %}

