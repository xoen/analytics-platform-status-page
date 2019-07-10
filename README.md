# Analytical Platform Status Page
This is the repository containing the Analytical Platform status
page.

The static website is under the `/analytical-platform` directory.

The static website is generated using [Hugo](https://gohugo.io/)
a popular static website generator.

The Status Page use the [cState](https://github.com/cstate/cstate)
which also provide the "issue" archetype.


## Hugo installation
On a Mac you can hugo by running `brew install hugo`, alternatively you
can follow the [installation instructions on the Hugo website].

[installation instructions on the Hugo website]: https://gohugo.io/getting-started/installing/


## Creating a new incident

### Creating the incident page
> Incidents are simply Markdown files (like test-issue.md) that are
> under content/issues/. They are formatted in such a way that cState
> can recognize the inputted data and generate your status page
> appropriately.

To create a new incident copy the [`content/issues/YYYY-MM-DD-template.md`](/analytical-platform/content/issues/YYYY-MM-DD-template.md) file:

```bash
# remember to tweak the destination filename
$ cp analytical-platform/content/issues/YYYY-MM-DD-template.md analytical-platform/content/issues/YYYY-MM-DD-incident-slug.md
```

Then edit this newly created file updating the following fields
as necessary:
- `title`, title of the issue, e.g. "DB Connection Issues"
- `date`, ISO-8601 formatted date when the incident was first discovered - including the seconds. (required)
- `resolved`, boolean, `true` when an issue is resolved
- `resolvedWhen`, date when the issue was resolved (required if `resolved` is `true`!)
- `severity`, can be `notice`, `disrupted` or `down` (from lower to higher severity)
- `affected`, list of systems affected, e.g. `Control Panel` or
  `Kubernetes Cluster`
- `section`, is always `issue` (don't change it)
- `published`, boolean which determine if the incident page is published

The details of the incident will go under `---` (there are some
example issues under [`content/issues/`](/analytical-platform/content/issues/)).

Note the use of the `{{< track "2019-01-01 15:56:00" >}}` shortcode which
will be displayed nicely in the rendered page - just remember to include
the seconds.

Remember to change `published: true` when you're happy with
the incident content.


See: [cState documentation on creating a new incident](https://github.com/cstate/cstate/wiki/Usage#creating-incidents-method-1).

### Testing Status Page locally
You can see how the Status Page will look like by running the Hugo
server locally.

From the [`/analytical-platform/`](/analytical-platform/) directory
run the following command:

```bash
$ hugo server
```

Then go to [http://localhost:1313/](http://localhost:1313/) in your
browser (or at whatever URL/port Hugo will run at).


### Publish the Status Page
**TODO**


## The "issue" archetype
The "issue" archetype is just a custom page type with the following
attributes:


## Systems
Systems are high level (ish) components. Users may want to know if
these are operational or not.

At the moment we only have the following Systems:
- `Control Panel`
- `Kubernetes Cluster`

We may want to add more or tweak the description. This can be done
updating the `params.systems` configuration in the [`/analytical-platform/config.yml`](/analytical-platform/config.yml) file if necessary.

**NOTE**: When using these in the `affected` field of an issue be sure
that the case is the same.

## Custom Tabs
Custom Tabs are shown in the page and we use them to link to the status pages of the following services:
- Auth0
- AWS
- GitHub

Again, if necessary this list can be changed by changing the `customTabs`
configuration in the [`/analytical-platform/config.yml`](/analytical-platform/config.yml) file.


## cstate documentation
For additional information you can look at the cState wiki at https://github.com/cstate/cstate/wiki
