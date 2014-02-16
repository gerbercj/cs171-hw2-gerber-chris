# 1. For each of the 5 visualizations (contributors, commits activity, code frequency, punch card, pulse) plus the calendar map, answer the following questions:

  * Who is the audience? (e.g. project manager, contributor, project user, visitor, etc.)
  * What data have been used? How can you get the data using the GitHub API? (Note that it can be the combination of multiple queries and their processing).
  * Those visualizations are updated over time. What happens if suddenly a contributor pushes many commits in a short time interval? How would you address this particular issue?

## Calendar map

This view would be useful for a visitor, to gain a sense as to how actively a project is being worked on. It might also be an interesting overview for a project manager.

This is likely implemented by calling `GET /repos/:owner/:repo/events`, and then grouping the events on `created_at`.

If multiple commits were pushed over a short interval, I probably would not do anything different, as this should naturally be grouped by pull request.

## Contributors to a repository

This view would be useful for a project manager, a project contributor, or a project user. It provides an entry point to ask questions about the project.

This is likely implemented by calling `GET /repos/:owner/:repo/stats/contributors`.

Again, I would not do anything differently if multiple commits were received during a short time frame.

## Commits Activity

This view would be useful for a visitor or project manager, to determine if the project is actively being developed, or if activity is winding down.

This is likely implemented by calling `GET /repos/:owner/:repo/stats/commit_activity`.

Again, I would not do anything differently if multiple commits were received during a short time frame.

## Code Frequency

This view would be useful for a visitor or contributor, to determine if the project is early in its development (heavy on adds), or mature in its development (increase in deletes shows refactoring).

This is likely implemented by calling `GET /repos/:owner/:repo/stats/code_frequency.

Again, I would not do anything differently if multiple commits were received during a short time frame.

## Punch card

This view would be useful for a project manager, to determine when developers were most productive.

This is likely implemented by calling `GET /repos/:owner/:repo/stats/punch_card`.

Again, I would not do anything differently if multiple commits were received during a short time frame.

## Pulse of a repository

This view would be useful for a visitor or project manager, to determine if the project is actively being developed, and if issues are being addressed in a timely manner.

This is likely implemented by calling `GET /repos/:owner/:repo/issues/events`, and parsing the returned data.

If multiple commits were received in a short time frame, it may be useful to aggregate them, or to simply filter the list to the N most recent items.

# 2. Looking at the network graph, answer the same questions as above, plus:

  * What is the role of interaction for this visualization? Would a static graph have been sufficient?
  * What happens if many new developers suddenly join the project and push commits for the first time? How would you to preserve the graph''s readability in such a situation?

This view would be most useful to a project contributor, to see how different commits have merged into the project over time.

This is likely implemented by calling `GET /repos/:owner/:repo/commits`.

If multiple commits were received in a short time frame, it would be useful to combine them into a single point, except in cases where they have arrows to other branches. We would then update the pop-up to show the multiple commit messages.

The interactive element removes unnecessary clutter from the display. By only showing commit details on hover, the graph itself stays very clear and uncluttered.

In this case, there would be many more vertical rows to look at. It might be more useful to make the first new commit the same color as the node that is came off of, to make it easier to follow the lines across accounts. It would also be useful to use the order of the timestamps to shift the vertical lines slightly so that they do not all overlap.

