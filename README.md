## What is StackAid?
A monthly subscription to StackAid funds your direct and indirect dependencies by analyzing your project configuration (eg: `package.json`).

**Interested in early access to StackAid? [Get in touch](https://www.stackaid.us/invite)**

## Why doesn’t open source funding work today?
The problem isn’t a lack of means or desire. Decision paralysis as well as the mechanics of paying are the dam holding back open source funding. Any trivial project can have a dozen dependencies and many more indirect dependencies. If you decide to fund your direct dependencies, here are the questions you then have to answer:

- How much should I give to each project?
- How do I fund each of these projects?

Assuming you’ve figured out those questions, you might still be wondering if this is workable. Will everyone else, especially the dependencies you fund, go to this effort to fund their dependencies? Probably not.

## How does it work?
The monthly subscription amount you choose is divided evenly across all your direct dependencies. Each direct dependency then automatically shares up to half of its allocation with its dependencies.

Let’s make this concrete:
```json
{
  "dependencies": {
    "bootstrap": "^5.1.0",
    "sass": "^1.38.0"
  }
}
```
With a current subscription of $25/month, `bootstrap` and `sass` are both allocated ($25 * 12 / 2) = $150/year. `sass` has 3 dependencies and so it shares up to 50% of it’s allocation with its dependencies, each capped at 5%, and `sass` is left with the difference. Since `bootstrap` has over 20 dependencies it shares the full 50% of its allocation equallly among them.

Here's the allocation breakdown:
```
sass/dart-sass (3)           $129/yr
├ paulmillr/chokidar           $8/yr
├ immutable-js/immutable-js    $8/yr
└ 7rulnik/source-map-js        $8/yr
twbs/bootstrap (41)           $75/yr
├ postcss/autoprefixer         $2/yr
├ babel/babel                  $2/yr
├ bundlewatch/bundlewatch      $2/yr
├ clean-css/clean-css-cli      $2/yr
├ kentcdodds/cross-env         $2/yr
└ 36 more
```

Play around with our [allocation tool](https://www.stackaid.us/audit) to see how funding your dependencies could work.

## How much does it cost?
Subscriptions start at $25/developer/month.

## How do you make money?
When you add your project dependencies, StackAid is treated as an implicit direct dependency. StackAid is on equal footing, but unlike those dependencies, StackAid's allocation is capped at 5%.

## I have two dependencies, `react` and `leftpad`. Is it fair that they get the same allocation?
No, it’s not fair.

However, across many subscriptions react is far more popular than leftpad and so the imbalance is sorted out.

## What happens when an open source project hasn’t claimed their allocation?
A project's allocations accumulate for 2 months. If the project is not claimed by then, an automatic reallocation happens and the amount is redistributed to the other dependencies that are claimed. Reallocation occurs on a per subscription basis.

## How do you know this model works?
While it’s easy to understand how a single subscription is distributed, it’s hard to tell if this is fair and meaningful. We had the same question, so we [built a simulation](https://simulation.stackaid.us/projects) of 5,000 subscribers at $25/month for a year.

The bottom line is that the long tail is pretty fat. Popular projects do well, but StackAid funds many more projects that would otherwise get overlooked.

## How is money distributed to an open source project?
An open source project can associate one or more Stripe accounts to their StackAid project. The allocated money is split between those Stripe accounts. The Stripe account can belong to a single person or an organization that has its own rules for how the money will be put to use.

## How does StackAid figure out my dependencies?
StackAid’s GitHub app searches your repositories for package dependency files. For example, for JavaScript projects we look for `package.json` files.

## How can I fund a project not in my package dependency tree?
You can provide a `stackaid.json` file that lists the repositories to treat as direct dependencies. For example, if you wanted to allocate money to the Linux kernel and NodeJS, then you would add these two repositories to your `stackaid.json` file:

```json
{
  "dependencies": [
    "https://github.com/torvalds/linux",
    "https://github.com/nodejs/node"
  ]
}
```
