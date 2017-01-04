---
title: The Fractal Nature of Software Estimation
date: 2017-1-03

---

Inspired by the excellent quora answer: https://www.quora.com/Why-are-software-development-task-estimations-regularly-off-by-a-factor-of-2-3/answer/Michael-Wolfe I noticed something. Doubtlessly to be read between the lines, but not explicitly mentioned, the shape of the coast is fractal in nature, at least up until a point. Each successive order of magnitude approximates the level of detail of the last, yet if we keep going we find that the smooth curves of an inlet are approximated by rocky crags.

Software estimation seems to me to have a similar feature. Tasks are estimated recursively (either explicitly or by estimation) by breaking up tasks into subtasks which are easier to estimate. At last we either end up with atomic tasks which are relatively difficult to estimate improperly. We can then estimate them and merge them all together into a list, or a directed acyclic graph depending on how complicated your project management software is. This process works for sorting a list of integers, why shouldn't it work for estimating software? If it doesn't work, is there some better method?

The process is:
1. Break into subtasks
2. for each subtask either:
2.1 estimate it if it is atomic
2.2  break it up further
3. check if we are done or recurse on the non-terminal nodes

The reason this path is lined with peril is, at the very least, a function of the inaccuracy of any given step. If we break a task into the wrong subtasks, we can expect there to be some kind of cost in either maintenance or inefficient development. We could have too many subtasks, not enough subtasks, etc... all of which could lead to a non-linear number of inaccuracies down the road (if you forget a subtask you now have possibly multiple levels in the graph that need to work the process). If we incorrectly classify tasks as small enough to estimate, we are left with a similar situation as before. Something could be missing, but it could actually be several levels in the graph, not just a constant error.

As it's obvious from the recursive nature of the problem, any of these hidden chunks of work that remain to be completed are liable to have their own inaccuracies involved with estimation. Very quickly you can begin to sense that there is a challenge in estimating software properly without even getting into the specifics of software itself. But this same level of complexity should be present in any workflow based on dependent tasks. Why is software seemingly worse off than other areas?

In addition to hidden layers of inaccurate estimation, we are also plagued with difficulty in even conceptualizing software in this manner in the first place. Changes to one subtask may obviate the need for other subtasks altogether. Or more commonly, a failure to understand some aspect of the problem domain makes obsolete work that was already completed.

The dependencies between these tasks are also tied to complex graphs of technical dependencies involved with the choice in implementation. We now have a mapping between two fractal webs of complexity that are liable to change at any time during the lifetime of the project. It's a wonder we're even as good at software estimation so as to misestimate by 2-3x times!

From here it's understandable that movements like agile seek to reduce any given project to the minimum set of requirements which are needed given the current state of the world, and to constantly reprioritize these or rewrite them given new evidence. I'm not an agile fanatic, but I do favor iteration over lengthy estimation. With agile we are not necessarily eliminating the complexity of the task/implementation graphs, but we're trying to purposefully examine only a small segment of them at any given time through the lens of business value.
