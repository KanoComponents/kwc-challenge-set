# \<kwc-challenge-set\>

## Purpose
To display a set of challenges for the user to complete.

 ## Properties
 * avatarUrl: The url of the current user's avatar. If none given a default icon is used.
 * challengeSet: The data for the challenge set to build a progress bar for.
 * completeIconUrl: A url to use for completed challenges in the progess bar.
 * currentIconUrl: A url for an icon to use for the current challenge in the progress bar.
 * lockedIconUrl: A url for an icon to used for locked challenges on the progress bar.
 * progress: A number representing the number of challenges in this set that are completed.
 * radius: The radius of each challenge progress circle in the progress bar.

The `challengeSet` property has the shape (specified using [json schema](https://spacetelescope.github.io/understanding-json-schema/)):

```js
// challengeSet
{
    type: 'object',
    properties: {
        title: {
            type: 'string'
        },
        description: {
            type: 'string'
        },
        category: {
            type: 'string'
        },
        medal-disabled:{
            type: 'string',
            format: 'url'
        },
        medal-enabled: {
            type: 'string',
            format: 'url'
        },
        challenges: {
            type: 'array',
            items:{
                type: 'object',
                properties: {
                    title: {
                        type: 'string'
                    },
                    slug: {
                        type: 'string'
                    }
                },
                required: [ 'title', 'slug' ]
            }
        }
    }
}
// e.g
{
    "title": "Flash and draw the lights",
    "description": "Turn on lights, change colors.",
    "category": "kano-code-challenges-pixel-intro",
    "medal-disabled": "static/challenges/training/pixel_medal_disabled.svg",
    "medal-enabled": "static/challenges/training/pixel_intro.svg",
    "challenges": [
        {
            "title": "Pixel lights on",
            "slug": "pixel_intro_1"
        },
        {
            "title": "Pixel color picker",
            "slug": "pixel_intro_2"
        },
        {
            "title": "Pixel color random loop",
            "slug": "pixel_intro_3"
        },
        {
            "title": "Pixel point",
            "slug": "pixel_intro_4"
        }
    ]
}
```


## Events
This component will fire a custom event `open-kano-code` intitated by a click or tap event on any of the challenge circles or the continue button. The event is passed the following detail:
```js
{
    type: 'object',
    properties: {
        type: {
            type: 'string'
        },
        challengeId: {
            type: 'string'
        }
    }
}
```
The challengeId can then be accessed in any listener implementation on the event detail property.
```js
addEventListener('open-kano-code', function(e){
    console.log(e.detail);
}
// e.g. {"type": "challenge", "challengeId: "pixel_talking_mouth"}
```

## Installation
* Clone this repository.
* Run `bower i`
* Make sure you have the [Polymer CLI](https://www.npmjs.com/package/polymer-cli) installed. Then run `polymer serve` to serve your element locally.

## Running Tests

```
$ polymer test --skip-plugin junit-reporter
```
