<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/metascan-engines/engine-scoring-with-post-action -->

# AV scoring with post action

If certain engines frequently produce false positive detections, you can use the "Post Action" feature (available in MetaDefender Core 5.8.0 and later) to execute a script that modifies the final verdict. Within the script, you can implement logic to assign high scores to specific engines and low scores to others.

**Step 1:** The "Post Action" script can only set the final verdict to infected and NOT clean. This means if you want to fully rely on scoring for the AV engine results, you have to set the infected AND suspicious AV thresholds to at least the number of your AV engines in your workflow under the Metascan tab.

**Step 2:** Download the scripts at [OPSWAT Github](https://github.com/OPSWAT/postaction-av-scoring) and follow the readme (This project is just an example, use and modify it at your own risk)

Technically, you create a post action, for example, on Windows:

**Step 3**: Configure a workflow to use this post action.
