# Roulette System Catalog Data Entry Guidelines

This repository is the set of guidelines for updating the Roulette System Catalog available on [jackace.com](https://www.jackace.com/gambling/roulette/systems/).

## Quick Links

* [Roulette System Queue (pick the oldest first)](https://github.com/JackAce/staging.jackace.com/issues?q=is%3Aissue+is%3Aopen+sort%3Acreated-asc)
* [Roulette System JSON Template](https://gist.github.com/JackAce/45ffe199d1c9a58a8ceaf3a87ebbd0a4)
* [Main Site - Roulette System Catalog](https://www.jackace.com/gambling/roulette/systems/)
* [GitHub Repository and Branch (feature/upworkupdates) to be Updated](https://github.com/JackAce/dev.jackace.com/tree/feature/upworkupdates)
* [Editing the Betting Tier image](betting-tier-image.md)
* [Reviewing Roulette System Changes](reviewing-system-changes.md)

## Repository

The GitHub respository you should be working from is [dev.jackace.com](https://github.com/JackAce/dev.jackace.com).

## Issues (Work Queue)

![GitHub Repository Issues](img/050-github-issues-600x300.png)

The queue for systems that need to be added are found in the Issues tab for the [dev.jackace.com repository on GitHub](https://github.com/JackAce/dev.jackace.com/issues?q=is%3Aissue+is%3Aopen+Add+spin+data+sort%3Acreated-asc).

Filter this list on "Add spin data" and sort the list by oldest first.

Click on the link for the issue to see the details.

### Issue Details
![GitHub Issue displaying system details](img/100-github-issue-600x196.png)

In the Issue Details, you should find the following:
* System Name
* Air Date
* YouTube URL of video reviewed

In the example above, this corresponds to 
* System Name: "Split the Hole"
* Air Date: "2024-11-29"
* YouTube URL: "https://www.youtube.com/watch?v=FY20XCfKIh0"

## JSON Item Template (Gist)

You can copy a template of a Roulette System item from the following [Gist](https://gist.github.com/JackAce/45ffe199d1c9a58a8ceaf3a87ebbd0a4).

![GitHub Gist of JSON Slug](img/200-gist-json-slug-600x580.png)

## Inserting a new JSON element

Before you start working in the branch, make sure you have the latest version. If you're just editing the file on GitHub's website, you should be mostly fine, but don't go too long without saving. If I merge changes while you're working directly on the file, you may run into conflicts.

Insert the Gist into the correct `data` file. Systems are broken apart according to the year it aired. So, for this example, we would append the JSON slug into the file `_data/roulette-systems-2024.json`.

The JSON goes into the Bracketed Array (`[]`) at the top of the file (assuming that the air date is more recent than any existing system). If you are inserting an older system, make sure you preserve the reverse chronological order (newest items on top).

Make sure you update the fields to the appropriate value.

* The `name` value should be the name specified in the GitHub Issue
* The `airDate` value should be the date specified in the GitHub Issue
* The `youtubeUrl` value should be the URL in the GitHub Issue
* For `reviewUrl`, start with the `airDate` value and append the `name`, separated with a hypen (`-`) and using hyphens instead of spaces. Preserve any existing capitalization. Ignore any punctuation and do NOT put two hypens together. So the `name` "Split the Hole" for the `airDate` "2024-11-29" would result in the `reviewUrl` "2024-11-29-Split-the-Hole".
* You can leave `rbaImageUrls` untouched with the single existing value.
* For `bettingTiers`, I will show you how to generate the JSON that goes here later on.
* For `systemType`, put the appropriate value if it is known. If it is *NOT* known, then leave this as "Other". Possible values include the following:
    * Flat Bet
    * Positive Progression
    * Negative Progression
    * Martingale
    * Ladder
    * Multi-Leg
    * Other
* The `buyIn` should be the Buy-in amount specified at the beginning of the video.
* For `bets`, update the existing value `6969` with the size of the first bet of the system. If you can determine the other bets in the system, you can add them here with each value separated with a comma (`,`).
* For the `rating`, you can update this with the rating that Alex gives at the end of the video. If Alex is not present and there is another presenter of the system, use that person's rating here instead. The valid values for the `rating` are "a" (Grapefruit), "b" (Peach), "c" (Plum), "d" (Eggplant), and "f" (Durian). Make sure you use the lowercase letter here. If you don't know the rating, just leave this value blank (`""`).
* Leave the rest of the fields at the default value until you get to `spins`.

Here's an example of what the JSON looks like for the given example:

```js
    "name": "Split the Hole",
    "airDate": "2024-11-29",
    "youtubeUrl": "https://www.youtube.com/watch?v=FY20XCfKIh0",
    "reviewUrl": "2024-11-29-Split-the-Hole",
    "rbaImageUrls": [
      "00-rba-0-800x768.png"
    ],
     "bettingTiers": [
      {"wheelType":1,"wagers":{"x12-doz1":60,"x12-doz3":60,"x2-17-20":15,"x2-0-00":15}}
    ],
    "systemType": "Flat Bet",
    "buyIn": 500,
    "bets": [
      150
    ],
    "rating": "c",
```

## Betting Tiers

To generate the JSON used for the betting tier(s), you should use the [JackAce Roulette Bet Analyzer](https://rba.jackace.com/).

![Roulette Bet Analyzer](img/400-rba-full-600x682.png)

Enter the bets as laid out by Alex at the beginning of the video. Click on the casino chip value and click on the bet being made.

### Recording Betting Tiers for "Multi-Tier" Strategies

**NOTE:** If this system is a "Multi-Tier" system, you *only* need to record the FIRST betting tier. A "Multi-Tier" system is a
system where multiple bets increase or decrease according to how that individual bet performs.

For example, you might have a system where you bet one unit each on Red and Even at the same time. If a bet loses, then you Double
the bet. If a bet wins, then you reset to 1 unit. This can result in a TON of different permutations that would be nearly impossible
to track. You only need to record the results for the first tier under `bettingTiers`.

![Curly Brackets](img/405-rba-brackets.png)

Once the bet is complete click on the curly brackets on the lower-right part of the screen. You may need to hide the GoogleAds at the bottom of the web page to see the text box that appears.

![JSON Output](img/410-rba-json.png)

Here's an example of the JSON generated for the "Double Street Martingale" bet ($125):
```js
    {"wheelType":1,"wagers":{"x6-4-9":25,"x6-10-15":25,"x6-16-21":25,"x6-22-27":25,"x6-28-33":25}}
```

Copy the JSON and replace the JSON that is in the `bettingTiers` array. If there are multiple betting tiers to define, then separate each one with a comma (`,`)

Here's an example of the `bettingTiers` section of the JSON with two bets inserted:

```js
     "bettingTiers": [
      {"wheelType":1,"wagers":{"x12-doz2":20,"x12-doz3":30}},
      {"wheelType":1,"wagers":{"x12-doz2":20,"x12-doz3":70}}
    ],
```
## Spins

Watch the YouTube video and record the data for every spin to the best of your ability. You should even record spins where no bet is made and spins where Alex does not bet.

You should be recording the following values:
* `spin` - The sequential number of the spin for the video
* `number` - The Roulette number that hits
* `amountBet` - How much Alex bets. If Alex isn't the main bettor, then it is the bet of the main bettor for the video.
* `result` - The NET win/loss result. This is how much they won or lost AFTER you subtract losses. So if you bet `100` on Black and you win, you would put `100`, not `200`.
* `time` - This is the timestamp of the FIRST FRAME where the video displays the win or loss. If the spin is not documented, then estimate this as best as possible. It is 10 times better to be 1 second early than it is to be 1 second late...but try to be accurate here.
* `notes` - This is usually omitted, but be sure to include a note if there are any discrepancies. For example, the video displays -100, but you know the bet was only 50, so that would be impossible. Record the *CORRECT* `result` and `betAmount` to the best of your ability and put any corrections in the `notes` field.

## Create the System Details File

Going back to the `reviewUrl` field, you want to create a file with a similar name in the `/gambling/roulette/systems/` folder. If the `reviewUrl` is "2024-11-29-Split-the-Hole", then you should create the file `2024-11-29-Split-the-Hole.html`.

You don't need to do much here. You can just use the following template:
```
---
layout: roulette-system
title: [SYSTEM_NAME_GOES_HERE] - Roulette System Review
---
```
for example

```
---
layout: roulette-system
title: Split the Hole - Roulette System Review
---
```

## Committing and Reporting

After you commit your changes to the `feature/upworkupdates` branch, please notify me via [Upwork messaging](https://www.upwork.com/ab/messages/).
