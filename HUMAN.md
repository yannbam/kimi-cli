# HUMAN NOTES — DO NOT EDIT!!!!

brilliant feature idea:
inspired by the denwarenji mail 
think loom 🌳! (weaving multiple branches from a checkpoint - see pyloom etc.)
example: implement three different approaches to a feature
then from a meta-perspective compare the end-results (checkpoint-leafs)
find the optimal candidate or maybe a fourth approach by combining the best-of branches
===> implement, save in files, and then denwarenji back 


----

## Intelligent Rolling Context Window
think rolling window, but refined:
- don't simply remove earlier context, but gather into summary/memory
- first ~1/5th (or so) of context is a summary/highlights (don't make it slop - make it high-signal / high information density => what was really important/salient in that context) of previous context
- thresholded rolling: to avoid invalidating the cash, roll at thresholds or even better: let kimi decide and choose the rolling points at clean points like having finished a task