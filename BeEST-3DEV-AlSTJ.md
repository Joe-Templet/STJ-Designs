# Design of New STJs for DES

Originally, these STJs were to be new AlSTJs for the BeEST, now the project encompasses more universal updates to the STJ design which helps with nuclear science in general, regardless of the layers chosen.

## Notes on Repo Management

Tracked files include Subproject specific files (Projects), Project specific reference material (Reference), and working design files organized by design platform (AutoCAD $\rightarrow$ KLayoutEditor $\rightarrow$ XIC).

Export includes drawing sheets and mask files (XIC GDS). Drawing sheets don't need to be tracked in this repo as they should be reproducible from some state of the design files that are tracked. The mask files are a form of tracked work themselves, and so it may be nice to track export versions in a separate repo elsewhere, if you'd like.

### Branching: Subprojects

It is recommended to create a subproject branch for work in development. As of updating this document, the only branch in this repo is the `main` branch. An `out` branch may also be prudent to associate output with this repository but in its own orphan branch.
Locally, I create branches at end-of-year marks so I can `git worktree` out a snapshot of the work completed in a given year, which is helpful for goal tracking and reporting.

Subproject branches should be merged back into `main` at certain milestones by a local git wizard. If solution-based committing is respected (see below), fast-forward merging is fine.

### Solution-Based Committing Strategy

Keep commits Descriptive and Atomic. Atomic commits solve a single problem with a single solution. They also separate out **All** rename actions from other actions (modify, delete, copy, add). Describe the problem and solution for each commit. These solutions don't have to be universal, any work can create a new bug, but so long as the intent of the commit is clear (what problem it attempted to solve from past work), debugging and future problem solving is made significantly easier. To ensure cleanliness in future merges to `main` it is wise to rewrite history, a fun albeit dangerous activity, before pushing to e.g. squash renames at your earliest local relevant commits. Consult a local git wizard or let them do the rewriting themselves if you are the least bit unsure about history rewriting.

---
## Active Projects



---
## Changelog

### 22-01-18 - (v1.3) - SiO2 Patching

This update brings my version of the fabrication file in sync with Robin's. It also provides SiO2 patches beneath each Nb upper probe, as the primary goal. I've done some refactoring while here, as well:

- New naming convention - see [[cell hierarchy]].
- More cells within cells, including:
	 - `TC` within `TC_B`
	 - `PRBE` Probe cells for both `TOP` (SiO2 and tapered probe) geometry, and `BTM` (plug/etch and tapered probe) geometry.
- Standardized probe and penetration depth across all chip architectures
	 - Added rectangles at base electrode interface, for easy alignment
	 - `TC` still has its own unique probe, but at least the penetration depths are synced.

--- 
## Connected Projects

%% Use this space to reference projects which rely on this project's internal subprojects as well as back-reference
imported (external) subprojects. %%
