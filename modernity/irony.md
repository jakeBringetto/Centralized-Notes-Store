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

## Irony, Post-Irony, Meta-Irony

The classic satire - Jonathan Swift's A Modest Proposal - has but one layer of irony (pretty pathetic if you ask me). His critique of Ireland and mistreatment of poor people is guised in the absurd idea of eating babies for food. Clearly, this wasn't meant to be taken literally. This is irony - when the "truth", or some underlying reality, or worldview, is portrayed as the opposite to reduce the something to absurdity, reinforcing what the author sees as "truth". It can also be extended to what we call "boomer humor", like those memes on boomer Facebook groups where a dude stands in front of his crashed car saying "my day is going great" or "lucky me" or something like that. But we've transcended now into a new realm of irony in which a new layer is placed on top of the "boomer level". Enter Post and Meta Irony. Their are some parallels here between this and modernism, post-modernism, and post-post-modernism or meta-modernism or trans-modernism... (see [page-1.md](../the-artist/page-1.md "mention")for more on things like this). Post-irony is a term describing a return to sincerity, where someone may say something they actually mean in a sarcastic way. Like "Come on guys, definitely think eating babies is a good idea" and actually liking the taste of babies (was John Swift post-ironic? I guess we'll never know). Meta-irony is again adding a layer of irony, but this time it's not really known what the speaker actually means. Maybe a guy who posts absurd things on 4chan "as a joke" but it's getting a little bit too habitual and detailed. Or John Swift actually not knowing if he supports eating babies. This true intent may be made unknown intentionally by the speaker, or it may even be that they themselves don't know what they mean. Like a guy pretending to be homeless on the street, and he actually starts living on the street. Is it still an act or is he actually just starting to be homeless.&#x20;

### Motivation and why?

It seems that post and meta-irony are actually very common literary tactics amongst
