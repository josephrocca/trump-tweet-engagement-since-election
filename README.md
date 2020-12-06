# Trump Tweet Engagement Since 2020 US Election

I was curious about the trend in engagement with Trump's tweets since the 2020 US election. Here's the code I used:

```js
let tweets = {};
let scrollInterval = setInterval(() => {
  [...document.querySelectorAll("[data-testid='like']")].forEach(el => {
    let timeEl = el.closest("[data-testid='tweet']").querySelector("a > time");
    let retweets = el.closest("[data-testid='tweet']").querySelector("[data-testid='retweet']").ariaLabel.split(" ")[0];
    let replies = el.closest("[data-testid='tweet']").querySelector("[data-testid='reply']").ariaLabel.split(" ")[0];
    let id = timeEl.closest("a").href.split("/").pop();
    tweets[id] = {
      time: new Date(timeEl.dateTime).getTime(),
      likes: Number(el.ariaLabel.split(" ")[0]),
      retweets,
      replies,
    };
  });
  window.scrollTo(0, window.scrollY + window.innerHeight/2);
}, 500);
//`date\tlikes\tretweets\treplies\n`+Object.values(tweets).sort((a,b) => a.time-b.time).map(o => `${new Date(o.time).toUTCString()}\t${o.likes}\t${o.retweets}\t${o.replies}`).join("\n");
```
Just paste that in your console when you're on a twitter profile page. It will eventually stop working when they change the UI, so the selectors may need updating depending on when you're reading this.

It seems like it only goes back to the 4th of November (811 tweets) without using advanced search date range features. Also, it's pretty crude because it also counts the likes of non-Trump tweets that Trump retweeted.

Here are some scatter plots of the data:

![Trump tweet likes since 2020 US election](https://i.imgur.com/GTFozRZ.png)


![Retweet counts on Trump tweets since 2020 US election](https://i.imgur.com/gUbNxjP.png)


![Reply counts to Trump tweets since 2020 US election](https://i.imgur.com/88pbzcI.png)

Note that some of the tweets have zero likes/retweets/replies, and this is because Twitter hid the contents of some of the tweets due to mininformation. I could have worked around this, but it's not a big deal - I was just looking for the general trend.

So it turns out that the data isn't (okay, *aren't*) that interesting. Engagement trails off after elections even for the winning candidate, which makes sense:

![Biden's tweet likes since 2020 US election](https://i.imgur.com/VZnIEzD.png)


