
**Fall Detection Unit Tests**

This project includes automated tests that validate the behavior of the `Fall_prediction` function using real image frames. The tests simulate different scenarios with **two** and **three** consecutive frames to confirm whether a fall should be detected or not.

### What these tests cover

The test suite checks fall detection outcomes for:

* **Two-frame detection**

  * Case 1: Two consecutive frames that should **not** represent a fall → expects `None`
  * Case 2: Two frames that **should** represent a fall → expects a result dictionary

* **Three-frame detection**

  * Multiple cases where a fall may occur between:

    * Frame 1 and Frame 2
    * Frame 1 and Frame 3
    * Frame 2 and Frame 3
  * One case where three frames should **not** represent a fall → expects `None`

### Expected output format

When a fall is detected, `Fall_prediction(...)` should return a dictionary containing:

* `confidence` — fall probability score
* `angle` — body inclination angle used for fall decision
* `keypoint_corr` — correlation/consistency score of pose keypoints

Each “fall detected” test verifies:

* `confidence > 0.3`
* `angle > 60`
* `keypoint_corr` exists (not empty)

When no fall is detected, the function should return:

* `None`

### Image loading

Images are loaded using Pillow (`PIL.Image.open`) from the `Images/` folder via a helper function `_get_image()`.

### How to run the tests

Install dependencies, then run:

```bash
pip install -r requirements.txt
pytest -q
```

Or run a specific test file:

```bash
pytest -q tests/test_fall_prediction.py
```

---

## If you want it as a docstring at the top of the file

Paste this at the very top of your `test_fall_prediction.py`:

```python
"""
ABOUT

This test suite validates the behavior of the Fall_prediction function using
real image frames. It checks fall detection using two and three consecutive
frames and ensures the function returns:

- None when no fall is detected
- A dictionary (with confidence, angle, keypoint_corr) when a fall is detected

For "fall detected" cases, the tests assert:
- confidence > 0.3
- angle > 60
- keypoint_corr is present

Run:
    pytest -q
or:
    pytest -q tests/test_fall_prediction.py
"""

