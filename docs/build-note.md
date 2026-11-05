# A missing issue is not necessarily a closed issue.

## The problem

A repository can have a long issue list without a clear next task. MaintainerOS turns a bounded activity snapshot into a local queue, with the evidence behind each suggestion.

## The decision and tradeoff

Store the capture policy with each snapshot instead of rescoring old history after a settings change. A comparison can then explain when its two scores were produced under different rules.

Sampling changes the meaning of a comparison. Items missing from a later sample are labeled no longer observed, rather than closed.

## Evidence from this review

Reviewed November 5, 2026 against source commit [fb1a2b6](https://github.com/hirsu-dev/maintaineros/commit/fb1a2b68e30dde5b1879ace5c2c8c55f833b662e).

- Environment: Windows; Python 3.12.14; SQLite 3.53.1.
- Result: **22 passed**.
- Command (from the repository root after installing the documented development dependencies):

```sh
python -m pytest -q
```

22 pytest checks passed on Windows, Python 3.12.14 and SQLite 3.53.1 on November 5, 2026. Network behavior is mocked in the automated tests.

The score is a transparent heuristic. The screenshot contains fictional demo projects; it is not evidence of real maintainers using the app.

## Walk through it

1. Start with a disposable demo database (the example repositories are fictional).
2. Change the capture policy and inspect two saved captures. The earlier capture keeps its own policy.
3. Use the policy tests to check that disappearing sampled issues are not described as closed.

## Still unfinished

Try the queue against real maintainer workflows and check whether the suggested tasks are useful. Large and rate-limited repositories still need broader evaluation.

## Source pointers

- [maintaineros/comparison.py](https://github.com/hirsu-dev/maintaineros/blob/fb1a2b68e30dde5b1879ace5c2c8c55f833b662e/maintaineros/comparison.py)
- [tests/test_policy.py](https://github.com/hirsu-dev/maintaineros/blob/fb1a2b68e30dde5b1879ace5c2c8c55f833b662e/tests/test_policy.py)

These notes describe the implementation and checks that can be reproduced. They do not claim independent users, target-device testing, or a personal experience that has not been supplied.
