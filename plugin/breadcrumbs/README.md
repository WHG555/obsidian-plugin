# Breadcrumb Trail

This plugin adds multiple new views to Obsidian.

### The [wiki](https://github.com/SkepticMystic/breadcrumbs/wiki) has more in-depth info on the plugin than the outdated readme.

You can find the changelog [here](https://github.com/SkepticMystic/breadcrumbs/blob/master/CHANGELOG.md).

## Basics

Breadcrumbs lets you add hierarchical metadata to your notes, then leverage that structure.
Using and up (↑), same (→), and down (↓) relationship, you can add directional structure to your notes.

## Matrix/List view

This view shows the current note's parents, siblings, and children in either of the following styles:

![image](https://user-images.githubusercontent.com/70717676/123402846-75a67f80-d5a8-11eb-8230-75c37441f122.png)

![image](https://user-images.githubusercontent.com/70717676/123402852-77704300-d5a8-11eb-8f56-c4eb3ca23e02.png)

To open the view in your sidebar, run the command `Breadcrumbs: Open View` from the command palette.

## Breadcrumbs Trail view

This view shows a trail of notes from the top of your vault down to your current note

![image](https://user-images.githubusercontent.com/70717676/123403044-a8507800-d5a8-11eb-9669-33148021b6fa.png)

To get this structure, the plugin requires that you use some type of metadata indicating the hierarchy of notes.
For example, you may have a yaml field called `parent`, which links to the current note's "parent" note: `parent: [[Parent Note]]`. (You can also use inline Dataview fields `parent:: [[Parent Note]]`).
Using this structure that you impose, you can use the breadcrumb trail to visualise the path back to your parent note.

## Feed my coffee problem

If you're so inclined, you can buy me a coffee over here: https://ko-fi.com/skepticmystic :)
