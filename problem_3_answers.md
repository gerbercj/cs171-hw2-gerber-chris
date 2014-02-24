# 1. Which graph-related tasks does an ideal GitHub Network Graph need to address?

The relevant tasks seem to be:

 * 4.1.3 - Find common connections
 * 4.1.4 - Find connectivity
 * 4.3.1 - Follow path

# 2. Get back to the GitHub network visualization you implemented and test it with the following projects on GitHub: D3, jQuery and Bootstrap. There's a lot more data, but the interaction patterns of users are also very different. What do you notice about the three repositories?

## D3:

We see authors are working on individual branches that are primarily merged in without interacting with other changes being merged. We also see that commits are merged in groups on a somewhat regular basis.

## jQuery:

Here we see one branch that all team members add commits to as they go. There are no merges to bring things back in.

## Bootstrap:

Here we see authors working on features in branches together, and then merging those features into a common release vehicle.

# 3. How does this impact your graph?

The Bootstrap graph winds up being very tall, as there are many smaller branches. The jQuery graph winds up looking like a straight line, as there is only one branch. The D3 graph falls between the two in depth.

# 4. How would you improve your visualization to address issues with the larger and more complex data?

It would be useful to visually reuse vertical space when two branches did not overlap in time, such as in `git log --graph --pretty=oneline`. It would also be useful to show different colors per contributor, rather than use both color and vertical position for the branch.

# Design Studio 1 notes

My goal, as a reviewer of code changes, is to see how much the code is changing over time. I came up with seven different visualizations, which look at the magnitudes of changes in different ways. While the idea of commits is useful, commits can be very different in numbers of files and lines of code changed. As such, it is difficult to see how much impact any individual commit has in the current GitHub visualization.

The visualization that most interests me, and seemed fun to build, is the one that uses zoomable sunbursts. This visualization should allow me to associate branches, authors, commits to lines changed, to see how much impact each is having.

