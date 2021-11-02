The SPACE Flow is a general purpose release first branch strategy.

It works for any version controlled software of any kind for any platform.

https://guides.github.com/introduction/flow/

https://git-scm.com/docs/gitworkflows

The motivation for this strategy is to start the development planning from the main goal, a version release.
Starting from this point, the team can think all things about the quest that is to release a new version instead of doing tasks only.

This simple flow is a result of our experience wit Git Flow and Github Flow
https://git-scm.com/docs/gitworkflows
https://guides.github.com/introduction/flow/

# **The master branch**

- The master branch always will have the **latest code released**.
- It's life time long, the same as the project.
- The master never won't trigger release pipelines. 
- The master just the most trustable source code with a **version tag**.

# **Release branches**
- They **always** branch **from master**.
- They should be **gone when merged** into master.
- A branch with the name beginning with "release" are triggers for CI/CD pipelines.
- The branch name is **release/{version}** where {version} starts with "v" and it's followed by a version string as in semver.org. 

**Example name:** release/v1.0.0

# **Feature branches**
- Like topic branches, they are short-lived.
- They should be **gone when merged** into release.
- The branch name is **feature/{name}** where name must express what Business feature is developed in it using [kebab-case](https://medium.com/better-programming/string-case-styles-camel-pascal-snake-and-kebab-case-981407998841)

**Example name:** feature/forgot-password

## **Remarks**
- It's a requirement to keep children branches updated when the have parallel branches in the same level. Merge upward immediately after an a download merge on a stable branch.
- Even though is possible and necessary work in different release versions in parallel, **NEVER** release a higher version before the release of a lower version.

<center>

 ![SPACE Flow](https://www.spaceneedl.com/flow/space-flow.png)
 
![image.png](/flow/space-flow.png =300x)

</center>

<!--
gitgraph

const graphContainer = document.getElementById("graph-container");
 
const options = {
  orientation : "vertical-reverse",
                mode: "compact"
};

// Instantiate the graph.
const gitgraph = GitgraphJS.createGitgraph(graphContainer, options);

// Simulate git commands with Gitgraph API.
const master = gitgraph.branch("master");
master.commit("Initial commit");

//release
const release = gitgraph.branch("release/v0.0.1");
release.commit("Release branch created");
release.tag("release/v0.0.1");

//feature1
const feature1 = release.branch("feature/chat");
feature1.commit("Feature branch created");
feature1.tag("feature/chat");
feature1.commit("Commit1");

//feature2
const feature2 = release.branch("feature/blog");
feature2.commit("Feature branch created");
feature2.tag("feature/blog");

//interpolation
feature1.commit("Commit2");

release.merge(feature1, "chat merged into release");

feature2.merge(release, "release merged into blog");

feature2.commit("Commit1");
feature2.commit("Commit2");




release.merge(feature2, "blog merged into release");

master.merge(release, "release/v0.0.1 merged into release");
master.tag("v0.0.1");
/*
const aFeature = gitgraph.branch("a-feature");
aFeature
  .commit("Make it work")
  .commit({ subject: "Make it right", hash: "test" })
  .commit("Make it fast");

release.merge(aFeature);
release.commit("Prepare v1");

master.merge(release).tag("v1.0.0");
*/

-->
