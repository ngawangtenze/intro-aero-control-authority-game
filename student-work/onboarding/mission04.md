# Separate trim, stability, and control

## Engineering question
A synthetic trainer condition is trimmed and statically restoring, but offers only 800 N m control capacity against a 1350 N m demand. Does it have sufficient initial pitch authority?

## Physics model
Trim indicator: net moment at the reference is zero. Stability indicator: restoring dCm/dalpha<0. Control indicator: margin=available-required.

## Inputs
Synthetic comparison: reference net moment=0 N m; dCm/dalpha=-0.6 per rad; available=800 N m; required=1350 N m. Indicators refer to their declared reference state.

## Outputs
output: Available minus required control moment

unit: N m

threshold: 0

control: Insufficient authority

explanation3: Available minus required moment (margin) directly compares what the elevator can produce with what the maneuver requires—a positive or zero margin means sufficient control, while a negative margin means insufficient. Zero starting moment (trim) only confirms the aircraft is currently balanced with no additional input; it says nothing about how much extra control moment is actually available when a response is commanded. A trimmed, stable aircraft can still lack enough control authority to execute a specific maneuver, exactly as shown here: trim and stability indicators can both look fine while the control margin is negative.

## Assumptions
Trim, stability, and control indicators answer different questions. The separate available-control increment is compared with the required-control increment.

## Validity
No dynamic stability or whole-flight-range control conclusion follows from these three static indicators.

## Predictions
Trim and restoring tendency can coexist with a negative control margin.

## Manual reference
Control margin=800−1350=−550 N m even though the other two indicators pass.

## Verification cases
At available=1350 N m the inclusive requirement is met exactly. At 800 it fails. A negative restoring slope cannot change that arithmetic.

## Feature requirements
Display three separate statuses; use a signed control margin with units and an inclusive zero threshold.

## Implementation
Sweep available control moment; compute available-required; compare with zero. Keep the trim and stability indicators unchanged.

## Decision
Withdraw the sufficient-control claim for this synthetic condition; trim and static stability alone are not proof of control.

## Recorded investigations
{
  "800": {
    "attemptId": "1a66aabe-25df-43d4-a0d4-133bb4919420",
    "at": "2026-09-13T07:58:36.898Z",
    "note": "At 800 N m available, the control margin is exactly -550 N m, which does not meets the requirement.",
    "evidence": "-550",
    "conclusion": "Insufficient authority",
    "readouts": [
      {
        "label": "Trim: reference net moment",
        "expression": "0",
        "unit": "N m",
        "value": 0
      },
      {
        "label": "Static restoring derivative",
        "expression": "-0.6",
        "unit": "per rad",
        "value": -0.6
      },
      {
        "label": "Available control moment",
        "expression": "available",
        "unit": "N m",
        "value": 800
      },
      {
        "label": "Required control moment",
        "expression": "required",
        "unit": "N m",
        "value": 1350
      },
      {
        "label": "Control margin",
        "expression": "available-required",
        "unit": "N m",
        "value": -550
      }
    ],
    "inputs": {
      "available": 800
    }
  },
  "1350": {
    "attemptId": "1a66aabe-25df-43d4-a0d4-133bb4919420",
    "at": "2026-09-13T07:57:19.183Z",
    "note": "At 1,350 N m available, the control margin is exactly 0 N m (1350 − 1350 = 0), which meets the requirement since equality satisfies the inclusive threshold. ",
    "evidence": "0",
    "conclusion": "Requirement met",
    "readouts": [
      {
        "label": "Trim: reference net moment",
        "expression": "0",
        "unit": "N m",
        "value": 0
      },
      {
        "label": "Static restoring derivative",
        "expression": "-0.6",
        "unit": "per rad",
        "value": -0.6
      },
      {
        "label": "Available control moment",
        "expression": "available",
        "unit": "N m",
        "value": 1350
      },
      {
        "label": "Required control moment",
        "expression": "required",
        "unit": "N m",
        "value": 1350
      },
      {
        "label": "Control margin",
        "expression": "available-required",
        "unit": "N m",
        "value": 0
      }
    ],
    "inputs": {
      "available": 1350
    }
  },
  "2000": {
    "attemptId": "1a66aabe-25df-43d4-a0d4-133bb4919420",
    "at": "2026-09-13T07:59:48.274Z",
    "note": "At 2000 N m available, the control margin is exactly 650 N m, which exceeds the requirement.",
    "evidence": "650",
    "conclusion": "Requirement met",
    "readouts": [
      {
        "label": "Trim: reference net moment",
        "expression": "0",
        "unit": "N m",
        "value": 0
      },
      {
        "label": "Static restoring derivative",
        "expression": "-0.6",
        "unit": "per rad",
        "value": -0.6
      },
      {
        "label": "Available control moment",
        "expression": "available",
        "unit": "N m",
        "value": 2000
      },
      {
        "label": "Required control moment",
        "expression": "required",
        "unit": "N m",
        "value": 1350
      },
      {
        "label": "Control margin",
        "expression": "available-required",
        "unit": "N m",
        "value": 650
      }
    ],
    "inputs": {
      "available": 2000
    }
  }
}

## Interpretation attempts
{
  "800": [
    {
      "correct": true,
      "feedback": "Your recorded value and choice match the calculation: Insufficient authority. Control margin: -550 N m. -550 < 0 Your instructor will review your explanation.",
      "attemptId": "1a66aabe-25df-43d4-a0d4-133bb4919420",
      "at": "2026-09-13T07:58:36.898Z",
      "conclusion": "Insufficient authority",
      "evidence": "-550",
      "note": "At 800 N m available, the control margin is exactly -550 N m, which does not meets the requirement.",
      "draftSnapshot": "{\"evidence\":\"-550\",\"conclusion\":\"Insufficient authority\",\"note\":\"At 800 N m available, the control margin is exactly -550 N m, which does not meets the requirement.\"}"
    }
  ],
  "1350": [
    {
      "correct": true,
      "feedback": "Your recorded value and choice match the calculation: Requirement met. Control margin: 0 N m. 0 = 0 Your instructor will review your explanation.",
      "attemptId": "1a66aabe-25df-43d4-a0d4-133bb4919420",
      "at": "2026-09-13T07:57:19.183Z",
      "conclusion": "Requirement met",
      "evidence": "0",
      "note": "At 1,350 N m available, the control margin is exactly 0 N m (1350 − 1350 = 0), which meets the requirement since equality satisfies the inclusive threshold. ",
      "draftSnapshot": "{\"conclusion\":\"Requirement met\",\"evidence\":\"0\",\"note\":\"At 1,350 N m available, the control margin is exactly 0 N m (1350 − 1350 = 0), which meets the requirement since equality satisfies the inclusive threshold. \"}"
    }
  ],
  "2000": [
    {
      "correct": true,
      "feedback": "Your recorded value and choice match the calculation: Requirement met. Control margin: 650 N m. 650 > 0 Your instructor will review your explanation.",
      "attemptId": "1a66aabe-25df-43d4-a0d4-133bb4919420",
      "at": "2026-09-13T07:59:48.274Z",
      "conclusion": "Requirement met",
      "evidence": "650",
      "note": "At 2000 N m available, the control margin is exactly 650 N m, which exceeds the requirement.",
      "draftSnapshot": "{\"evidence\":\"650\",\"conclusion\":\"Requirement met\",\"note\":\"At 2000 N m available, the control margin is exactly 650 N m, which exceeds the requirement.\"}"
    }
  ]
}

## Evidence status
Written reasoning awaits instructor review. This export is the current draft; compare it with the answer snapshot of the last run.

## Student reflection
Question: Even when the control margin is positive, what additional information would you need to predict how quickly the aircraft reaches a new pitch angle?

Included: The cases compare starting moment balance, a static restoring derivative, and available versus required control moment.

Omitted: They do not simulate how pitch angle and pitch rate evolve after a control input.

confirmedFor: 1a66aabe-25df-43d4-a0d4-133bb4919420

observation: At 800 N m available, the control margin was −550 N m — insufficient authority. At 1,350 N m, the margin was exactly 0 N m, meeting the requirement inclusively. At 2,000 N m, the margin was +650 N m, comfortably exceeding the requirement. Across all three cases, trim (0 N m reference net moment) and static restoring tendency (−0.6 per rad) stayed completely unchanged — only the control margin changed as available moment increased.

change: I confirmed that trim and static stability are separate questions from control authority, and that neither one predicts whether a specific control demand can be met. Even though the aircraft was trimmed and statically stable in every case, only the direct comparison of available versus required moment (margin) determined whether the 1,350 N m demand could actually be satisfied.

limit: "Even with a positive margin, I would need the aircraft's pitch moment of inertia (Iy) to convert the margin into an actual angular acceleration, then integrate that acceleration over time to find how pitch rate and pitch angle evolve.

result: supported