# vla-robustness-kit

`vla-robustness-kit` generates deterministic, simulator-free perturbation
diagnostics over episode instructions, metadata, and task-phase lists.

## At a Glance

| | |
| --- | --- |
| Job | Exercise a robustness-report pipeline across language, vision metadata, embodiment metadata, and phase-order variants. |
| Built for | VLA evaluation developers and robotics teams prototyping review workflows. |
| Differentiator | Runs without a simulator, GPU, robot, image transformation, or model service. |
| Produces | Markdown pass rates, failure clusters, and follow-up data collection recommendations. |

## Install

```bash
python -m pip install "vla-robustness-kit==0.1.2"
```

## Verified Quickstart

Run from a source checkout:

```bash
vla-robustness-kit run examples/mock_episode_set \
  --policy mock \
  --out /tmp/vla-robustness-report.md
```

The bundled fixture emits 22 deterministic perturbation trials and a Markdown
diagnostic report.

## What Is Actually Perturbed

- language instruction strings;
- lighting and camera-pose metadata;
- control-rate and coordinate-frame metadata;
- task-phase ordering.

The standalone CLI currently accepts only `--policy mock`. The bundled mock
policy assigns deterministic pass/fail outcomes from variant names and fixture
tags. It does not invoke a VLA model or inspect image pixels.

LeRobot and RLDS helper modules normalize selected metadata fields for callers,
but the CLI reads an `episodes.jsonl` file or a directory containing that file.

## Runtime, Data, and Network Boundary

- The CLI reads local JSONL and writes Markdown locally or to stdout.
- It does not make network requests, run a simulator, use a GPU, access robot
  hardware, or call a model.
- No redaction is applied. Instructions, metadata values, and episode IDs can
  appear in downstream trial data, so sanitize inputs before sharing.
- Pass rates from the mock policy validate the diagnostic plumbing only. They
  are not evidence of policy robustness or robot safety.

## Limitations

- The standalone CLI currently supports only the bundled mock policy and
  metadata-level perturbations. It does not transform images or execute a VLA.
- Reports diagnose the supplied fixture or episode set only. They are not
  benchmark scores, simulator results, or safety guarantees.

## Compatibility

`robostudio-engine` exposes a direct `robostudio probe` integration. Its wrapper
can run the bundled mock policy or an explicitly supplied local executable
adapter; that BYO executable path is an engine feature, not a capability of the
standalone `vla-robustness-kit` CLI.

## Publication Status

Verified on 2026-07-13:

- PyPI: [`vla-robustness-kit==0.1.2`](https://pypi.org/project/vla-robustness-kit/0.1.2/)
- GitHub release: [`v0.1.2`](https://github.com/auraoneai/vla-robustness-kit/releases/tag/v0.1.2)
- Bundled reports are deterministic tutorial diagnostics, not benchmark or
  deployment evidence.

## Next Action

Use the mock policy to validate report ingestion and review, then connect a
separately reviewed executable policy adapter through `robostudio-engine` for
real model outputs.
