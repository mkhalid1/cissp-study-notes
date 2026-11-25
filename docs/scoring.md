<!-- nav:top -->
[Contents](../README.md#contents) · Previous: [Domain 8: Software Development Security](sections/software-development-security.md) · Next: [Timing and pacing](timing.md)
<!-- /nav:top -->

# How CISSP scoring works

Short version: the CISSP is scored on a scale where 700 out of 1000 is a pass, but the computer decides pass or fail by estimating your ability as you go, not by counting how many items you got right. The exam stops when it is confident of the result, when you reach 150 items, or when the 3 hours run out.

## The passing standard

ISC2 states the passing grade as **700 out of 1000 points**. That is a scaled standard, not a percentage of items. Because the exam adapts to you, two candidates can see very different sets of items, so a simple percentage would not be fair. What matters is the difficulty of the items you answer correctly.

ISC2 does not publish a pass rate, the number of items per domain on any one exam, or a table converting answers to points.

## How the adaptive engine decides

From ISC2's description of its Computerized Adaptive Testing:

- You start with an item well below the passing standard.
- After each answer the system re-estimates your ability, using the difficulty of every item you have seen and whether you answered it correctly.
- Each new item is chosen so you have about a 50% chance of answering it correctly.
- Every exam contains **25 pretest items** that do not count. They are being trialled for future exams, and you cannot tell which ones they are, so treat every item as if it counts.

ISC2 makes a point worth remembering on the day: because items are targeted at your level, everyone gets roughly half of the items they see right. Feeling that you are getting many wrong is normal and does not mean you are failing.

## The three stopping rules

ISC2 applies these in order:

| Rule | When it applies | What happens |
|---|---|---|
| Confidence interval rule | After the minimum of 100 items | The exam ends as soon as your ability estimate is above or below the pass point with 95% statistical confidence. |
| Maximum-length rule | You reach 150 items without the first rule triggering | Your final ability estimate is compared with the passing standard. |
| Run-out-of-time rule | The 3 hours end without the first rule triggering | Your final ability estimate is compared with the passing standard. |

One extra condition: if you have not answered at least **75 scored items and 25 pretest items** within the time limit, you fail automatically. In practice, that means you must reach item 100 before time runs out.

## What the length of your exam means

Not much, on its own. An exam that stops at 100 items means the system was 95% confident, which can be a clear pass or a clear fail. An exam that goes to 150 means your ability was close to the standard, and the final estimate decides. ISC2 also notes that the difficulty of the last item tells you nothing reliable, because every item feels hard when it is targeted at your level.

## Why there is no going back

Because each item is chosen based on your previous answers, ISC2 does not allow item review. Once you finalise an answer it cannot be reviewed or changed. This changes how you should practise: train yourself to read once carefully, decide, and move on. The [timing guide](timing.md) shows how.

## Results

At a Pearson VUE test centre, the proctor gives you an unofficial result when you check out. ISC2 then emails the official result and, if you passed, directions for the next steps. ISC2 does not send a score report with item-level detail. See the [test-day checklist](test-day-checklist.md#afterwards) for what to do after a pass.

## Retakes

If you do not pass, ISC2's rules are:

| After attempt | Wait before retesting |
|---|---|
| First | 30 test-free days |
| Second | 60 test-free days from the most recent attempt |
| Third and later | 90 test-free days from the most recent attempt |

You can attempt an ISC2 exam at most four times within a 12-month period for each certification.

## What counts as good practice performance

Practice tests cannot reproduce ISC2's scaled score or its item bank, so no practice percentage converts to a pass. As our study guidance, not an ISC2 standard:

- Use practice sets to find **which domains** cost you points, then fix those.
- Review every miss with the method in the [study plans](study-plans.md#how-to-review-a-missed-item); the reasoning matters more than the score.
- Practise without going back, so the real exam's no-review rule does not throw you.

## Sources

- [ISC2 CISSP exam outline page](https://www.isc2.org/certifications/cissp/cissp-certification-exam-outline), for the passing grade, length and items
- [ISC2 CISSP CAT page](https://www.isc2.org/certifications/cissp/cissp-cat), for the adaptive engine, pretest items, stopping rules, item review and retakes
- [ISC2: after your exam](https://www.isc2.org/exams/after-your-exam), for unofficial and official results

---

<!-- nav:bottom -->
← Previous: [Domain 8: Software Development Security](sections/software-development-security.md) | Next: [Timing and pacing](timing.md) → | [Back to contents](../README.md#contents)
<!-- /nav:bottom -->
