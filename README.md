## What is StackAid?

StackAid is a simple way to donate to all the open source software projects you depend on. By subscribing to StackAid, we'll distribute your subscription fee among your projects' direct _and indirect_ dependencies based on your project configuration (eg: package.json).

**[Get Started](https://github.com/apps/stackaid)**

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

With a current subscription of $20/month, `bootstrap` and `sass` are both allocated ($20 \* 12 / 2) = $120/year. `sass` has 3 dependencies and so it shares up to 50% of it’s allocation with its dependencies, each capped at 5%, and `sass` is left with the difference. Since `bootstrap` has over 20 dependencies it shares the full 50% of its allocation equallly among them.

Here's the allocation breakdown:

```
sass/dart-sass (3)           $102/yr
├ paulmillr/chokidar           $6/yr
├ immutable-js/immutable-js    $6/yr
└ 7rulnik/source-map-js        $6/yr
twbs/bootstrap (19)           $60/yr
├ postcss/autoprefixer         $3/yr
├ babel/babel                  $3/yr
├ bundlewatch/bundlewatch      $3/yr
├ clean-css/clean-css-cli      $3/yr
├ kentcdodds/cross-env         $3/yr
└ 14 more
```

You'll notice above that sass earns $1/yr more than expected. This is because bootstrap also depends on sass so it receives an indirect dependency allocation from bootstrap.

Play around with our [analyze tool](https://www.stackaid.us/#analyze) to see how funding your dependencies could work.

## How much does it cost?

Subscriptions start at $15/developer/month.

## How do you make money?

When you add your project dependencies, StackAid is treated as an implicit direct dependency. StackAid is on equal footing, but unlike those dependencies, StackAid's allocation is capped at 7.5%.

## How does StackAid figure out my dependencies?

StackAid’s GitHub app searches your repositories for package dependency files. For example, for JavaScript projects we look for `package.json` files.

## Is StackAid only for Node.js/npm based projects?

No, you can use our [GitHub action](https://github.com/marketplace/actions/stackaid-dependency-generator) to automatically generate and publish a stackaid.json file which lists your dependencies.

You can of course manually curate the list of projects you want to fund. For example, if you wanted to allocate money to the Linux kernel and Node.js, then you would add these two repositories to your stackaid.json file:

```json
{
  "version": 1,
  "dependencies": [
    { "source": "https://github.com/torvalds/linux" },
    { "source": "https://github.com/nodejs/node" }
  ]
}
```

We are working on bringing the same level of automated discovery and integration for Node.js projects to other ecosystems.

## Can I use StackAid without giving read access to my source?

Yes, we recommend setting up a new repository that's just meant
to be shared with StackAid and then use our [GitHub action](https://github.com/marketplace/actions/stackaid-dependency-generator#funding-dependencies-in-sensitive-repositories)
to automatically publish your dependencies there for discovery.

## How does my open source project get paid by StackAid?

Owners of open source projects can claim their repositories by installing the StackAid GitHub app. As part of the claiming process, owners can associate one or more Stripe accounts with each repository they own to receive payments.

Once a month the money allocated for each repository is split evenly among the associated Stripe accounts.

Stripe accounts can belong to a single person or an organization that has its own rules for how the money will be put to use.

## What happens when an open source project hasn’t claimed their allocation?

A project's allocations accumulate for 2 months. If the project is not claimed by then, an automatic reallocation happens and the amount is redistributed to the other dependencies that are claimed. Reallocation occurs on a per subscription basis.

## How do you know this model works?

While it’s easy to understand how a single subscription is distributed, it’s hard to tell if this is fair and meaningful. We had the same question, so we [built a simulation](https://simulation.stackaid.us/projects) of 5,000 subscribers for a year.

The bottom line is that the long tail is pretty fat. Popular projects do well, but StackAid funds many more projects that would otherwise get overlooked.
