# Github Zoomable Sunburst Visualization

## Overview

This visualization addresses the need for a code reviewer to see how many lines of code are being changed by the various commits, authors, and branches in a repository. Individual arcs can be clicked on to zoom in to a scope, and the center can be clicked to zoom back out. This visualization makes it very easy to understand what changes have had the most impact, and which authors are making the most changes.

## Usage

By default, the graph will be populated with data from the Twitter Bootstrap repository. To switch to another repository it is currently necessary to edit the code. After the page loads it will take several seconds for the data to be downloaded and parsed. Once that is complete, the visualization will appear and can continue to be used without a network connection.

The visualization consists of the repository in the center, and rings surrounding it. As one moves out from the center they move through branches, authors, commits, and finally arrive at lines of code changed. Hovering over any arc shows the details for that arc. Clicking on an arc will zoom in to make that the center of the visualization, with the remaining subordinate nodes as rings around it. Clicking on the center zooms back out one level.

## Technical Decisions

I chose to implement the seventh of my sketches after discussing the ideas with my group. This visualization meets my criteria of showing how much each commit and each author were impacting a project using the metric of lines of code changed. I was happy to be able to include all of the categories that I had hoped to include and the visualization meets with my expectations.

One key techncial decision was around API calls. I found that I needed to use three different API's to obtain all of the data that I required. These calls need to be nested, and multiply out to several hundred requests. As such, the user needs to be authenticated to get a useful visualization to be displayed. Because of this, I have left a valid Github token in the project.

Another key decision was around how to handle authors having multiple commits. As the Github API does not group commits by author, I needed to perform the aggregation myself. This led to some hairy Javascript code where I use an associative array to deduplicate my author data. This takes some CPU time, but was ultimately still faster than all of the API calls, and seemed efficient enough for my purposes.

Finally, I chose to limit my commit data to 100 items. This is a limitation, but going much higher would lead to many more API calls, and to further performance impacts when rendering the zoom animations. This seems suitable for my purposes at this time.
