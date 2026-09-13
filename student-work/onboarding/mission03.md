# Respect derivative units and usable travel

## Engineering question
Using Chapter 6 Worked Example A, does a requested dCm=-0.25 lie within the usable positive elevator travel?

## Physics model
deltaRad=demand/slope; deltaDeg=deltaRad*180/pi. Here slope is per radian; positive elevator deflection produces a negative pitching-moment increment.

## Inputs
slope: -1.05

demand: -0.25

usableLimit: 18

explanation2: Both the slope and demand are negative because positive elevator deflection produces a negative pitching-moment coefficient change, and this task specifically requests a negative change. Dividing demand by slope cancels the negative signs and gives a positive number in radians, since the slope's units are 'coefficient change per radian.'

## Outputs
Required elevator deflection in rad and deg, remaining elevator travel in deg, and whether the angle fits the stated range.

## Assumptions
The local derivative is held fixed provisionally. The stated usable stop is a limit, not proof that the derivative applies throughout the travel.

## Validity
This calculation checks the elevator angle using a fixed local derivative. Actuator holding force, rate, nonlinear response and coupled limits remain unverified.

## Predictions
The required deflection should be positive and smaller than 18 degrees.

## Manual reference
(-0.25)/(-1.05)=0.238095 rad=13.6419 deg; residual=4.3581 deg.

## Verification cases
Retain the negative coefficient sign; use -1.05 per radian, not per degree; compare 13.6419 deg with the 18 deg usable limit.

## Feature requirements
Plot demand-derived deflection against coefficient demand and show the usable limit in degrees.

## Implementation
For each coefficient demand evaluate demand/slope*180/pi and compare with the supplied usableLimit. Do not substitute degrees into a per-radian derivative.

## Decision
Provisionally retain the travel comparison; request a coefficient-versus-deflection sweep and actuator data.

## Recorded investigations
{
  "-0.25": {
    "attemptId": "f2e2351a-b34f-49f0-b3bf-75f54c4fe6f5",
    "at": "2026-09-13T07:35:21.827Z",
    "note": "The required deflection is +0.2381 rad, which converts to +13.6419°. Since this is positive and falls between 0° and the 18° usable limit, it is within positive travel. The positive sign confirms the elevator must move in the positive direction to produce this negative coefficient demand .",
    "evidence": "0.2381",
    "conclusion": "Within positive travel",
    "readouts": [
      {
        "label": "Required deflection",
        "expression": "demand/slope",
        "unit": "rad",
        "value": 0.23809523809523808
      },
      {
        "label": "Required deflection",
        "expression": "demand/slope*180/pi",
        "unit": "deg",
        "value": 13.6418522650196
      },
      {
        "label": "Usable positive travel",
        "expression": "usableLimit",
        "unit": "deg",
        "value": 18
      },
      {
        "label": "Remaining positive travel",
        "expression": "usableLimit-demand/slope*180/pi",
        "unit": "deg",
        "value": 4.358147734980401
      }
    ],
    "inputs": {
      "demand": -0.25
    }
  }
}

## Interpretation attempts
{
  "-0.25": [
    {
      "correct": true,
      "feedback": "Your recorded value and choice match the calculation: Within positive travel. Required deflection: 0.2381 rad. 13.6419 < 18 Your instructor will review your explanation.",
      "attemptId": "f2e2351a-b34f-49f0-b3bf-75f54c4fe6f5",
      "at": "2026-09-13T07:35:21.827Z",
      "conclusion": "Within positive travel",
      "evidence": "0.2381",
      "note": "The required deflection is +0.2381 rad, which converts to +13.6419°. Since this is positive and falls between 0° and the 18° usable limit, it is within positive travel. The positive sign confirms the elevator must move in the positive direction to produce this negative coefficient demand .",
      "draftSnapshot": "{\"evidence\":\"0.2381\",\"conclusion\":\"Within positive travel\",\"note\":\"The required deflection is +0.2381 rad, which converts to +13.6419°. Since this is positive and falls between 0° and the 18° usable limit, it is within positive travel. The positive sign confirms the elevator must move in the positive direction to produce this negative coefficient demand .\"}"
    }
  ],
  "-0.35": [
    {
      "correct": false,
      "feedback": "Re-read “Required deflection”. Record its value in the labelled units (numbers within ±0.0001), then compare it with the criterion. Check the sign first, then compare the required positive deflection with the usable travel.",
      "attemptId": "f2e2351a-b34f-49f0-b3bf-75f54c4fe6f5",
      "at": "2026-09-13T07:38:27.098Z",
      "conclusion": "Outside declared positive travel",
      "evidence": "0,3333",
      "note": "The required deflection is 0.3333 rad, which converts to +19.0986 deg. Since this falls beyond 18° usable limit, it is not within the positive travel. ",
      "draftSnapshot": "{\"evidence\":\"0,3333\",\"conclusion\":\"Outside declared positive travel\",\"note\":\"The required deflection is 0.3333 rad, which converts to +19.0986 deg. Since this falls beyond 18° usable limit, it is not within the positive travel. \"}"
    }
  ]
}

## Evidence status
Written reasoning awaits instructor review. This export is the current draft; compare it with the answer snapshot of the last run.

## Student reflection
Question: What measurements would you need before trusting the same elevator effectiveness near the travel limit?

Included: The calculation uses a constant coefficient change per radian of elevator deflection and checks the required angle against the usable travel limit.

Omitted: It does not test whether that constant effectiveness remains accurate near the travel limit.

confirmedFor: 

observation: At demand −0.25, the required deflection was 13.6419°, which fits within the 18° usable positive travel with 4.3581° remaining. At demand −0.35, the required deflection was 19.0986 deg, which exceeds the usable travel.

change: I confirmed that both demands correctly produced positive required deflections, since the two negative signs (slope and demand) cancel consistently. I also confirmed that a larger magnitude demand (−0.35 vs −0.25) requires proportionally more elevator deflection, since the relationship is linear (deflection = demand/slope).

result: supported

limit: I would need actual measured coefficient-change data at deflection angles close to the 18° limit itself, rather than assuming the same −1.05 per radian slope holds true there. 