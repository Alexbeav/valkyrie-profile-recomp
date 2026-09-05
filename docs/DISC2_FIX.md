# Disc 2 load correction

Version 0.1.3 carries the timed CD lid correction from upstream
[psxrecomp PR 279](https://github.com/mstan/psxrecomp/pull/279).
Previously, selecting Disc 2 could show a successful host notification while
Valkyrie Profile continued to request Disc 2. The correction holds the virtual
lid open long enough for the game to observe the change and handles the lid
status and interrupt sequence.

## Evidence

On September 5, 2026, Alex reproduced the failure on the older local build,
then confirmed that the late-game save continued after selecting Disc 2 in
the corrected Windows trial. Trial executable SHA-256:
`AE0F4C352581F08D734F0145B8928CE5D7FD5B382E45A38360D9022C32402C58`.
This confirms the reported Disc 2 load route. It does not establish full-game
completion, every disc transition, or save/reload after the transition.

The public source retains the v0.1.2 packaging line and adds the same runtime
correction. The C11 lid-state test and Python integration guards pass on that
source. Public kit setup and platform checks are recorded separately from the
operator's private gameplay test. No private save or playable executable is
included in the release.

## Use

1. Supply the supported USA discs and required BIOS during setup.
2. Load the save using Disc 1.
3. When the game requests Disc 2, open F1, Disc, Change Disc.
4. Select the USA Disc 2 CUE and allow a few seconds for detection.

## Future runtime rebuild

Owner: Valkyrie Profile maintainer. This is a focused backport on the existing
release runtime. Rebuild on a newly selected psxrecomp revision with its newer
multi-disc support, then repeat this same late-game load, connected disc
change, and save/reload checks. Do not treat this test as acceptance of an
untested future runtime. Retire the backport only after the replacement passes.
