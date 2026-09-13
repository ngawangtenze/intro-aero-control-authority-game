# Challenge the local-flow assumption

## Engineering question
Can the freestream-based trainer authority estimate be reused when the elevator sees slower local flow?

## Physics model
M_baseline=0.5*rho*V²*S*c*dCm; M_local=0.5*rho*(flowFactor*V)²*S*c*dCm. Required control moment remains 1350 N m.

## Inputs
900 kg trainer; rho=1.20 kg/m³; V=20 m/s; S=27.25 m²; c=4 m; usable dCm=0.153; Iy=5000 kg m²; other=-750 N m; target=0.12 rad/s². Nose-up moment is positive about the declared CG. Teaching sensitivity parameter flowFactor=0.7; it is not a measured tail-flow value.

## Outputs
Freestream-based capacity, local-flow sensitivity capacity, and whether each exceeds 1350 N m.

## Assumptions
assumption: It assumes airflow at the elevator has the same speed as the undisturbed airflow.

consequence: Overestimates available authority

ratio: 0.49

explanation4: The original estimate assumes the air reaching the elevator moves at the same speed as the freestream flight speed (V), since the physics model uses V directly. If the actual local speed at the elevator is slower, the real available moment is smaller than the original estimate predicts, since moment scales with the square of speed.

## Validity
This factor study isolates speed sensitivity; real local flow may also change the usable coefficient. It does not independently validate tail aerodynamics.

## Predictions
A 0.7 local-speed factor gives 0.49 of the baseline capacity. A 0.5 factor may remove sufficient authority.

## Manual reference
At 0.7: available=1961.2152 N m and margin=611.2152 N m. At 0.5: available=1000.62 N m and margin=-349.38 N m.

## Verification cases
Compare factors 1, 0.7 and 0.5 with unchanged density, geometry, usable coefficient and moment demand.

## Feature requirements
Label the factor as a teaching assumption. Show baseline, adjusted capacity, demand and limitations.

## Implementation
At each flowFactor evaluate the two equations above; preserve the declared configuration and required moment.

## Decision
Request local-flow and coefficient evidence at the limiting alpha, flap/power state and loading; do not claim the freestream estimate is universally valid.

## Recorded investigations
{
  "1": {
    "attemptId": "d64ef73e-3a62-4216-b9cc-4bed5e870a1b",
    "at": "2026-09-13T08:10:41.865Z",
    "note": "At a local speed factor of 1, the local airspeed equals the freestream speed exactly, so the adjusted capacity (4,002.48 N m) is identical to the original capacity — no reduction occurs.",
    "evidence": "2652.48",
    "conclusion": "Requirement met",
    "readouts": [
      {
        "label": "Original capacity using flight speed",
        "expression": "0.5*rho*V^2*S*c*dCm",
        "unit": "N m",
        "value": 4002.48
      },
      {
        "label": "Capacity using local elevator airspeed",
        "expression": "0.5*rho*(flowFactor*V)^2*S*c*dCm",
        "unit": "N m",
        "value": 4002.48
      },
      {
        "label": "Required moment",
        "expression": "1350",
        "unit": "N m",
        "value": 1350
      },
      {
        "label": "Adjusted margin",
        "expression": "0.5*rho*(flowFactor*V)^2*S*c*dCm-1350",
        "unit": "N m",
        "value": 2652.48
      }
    ],
    "inputs": {
      "flowFactor": 1
    }
  },
  "0.5": {
    "attemptId": "d64ef73e-3a62-4216-b9cc-4bed5e870a1b",
    "at": "2026-09-13T08:15:35.386Z",
    "note": "At a local speed factor of 0.5, the local airspeed is only half of freestream speed, so the adjusted capacity drops to 1,000.62 N m — just 0.25 (0.5²) of the original capacity. This is now below the 1,350 N m required moment, giving an adjusted margin of −349.38 N m.",
    "evidence": "-349.38",
    "conclusion": "Insufficient authority",
    "readouts": [
      {
        "label": "Original capacity using flight speed",
        "expression": "0.5*rho*V^2*S*c*dCm",
        "unit": "N m",
        "value": 4002.48
      },
      {
        "label": "Capacity using local elevator airspeed",
        "expression": "0.5*rho*(flowFactor*V)^2*S*c*dCm",
        "unit": "N m",
        "value": 1000.62
      },
      {
        "label": "Required moment",
        "expression": "1350",
        "unit": "N m",
        "value": 1350
      },
      {
        "label": "Adjusted margin",
        "expression": "0.5*rho*(flowFactor*V)^2*S*c*dCm-1350",
        "unit": "N m",
        "value": -349.38
      }
    ],
    "inputs": {
      "flowFactor": 0.5
    }
  },
  "0.7": {
    "attemptId": "d64ef73e-3a62-4216-b9cc-4bed5e870a1b",
    "at": "2026-09-13T08:15:04.705Z",
    "note": "At a local speed factor of 0.7, the local airspeed is 70% of freestream speed, so the adjusted capacity drops to 1,961.2152 N m — only 0.49 (0.7²) of the original 4,002.48 N m capacity, since moment scales with the square of speed.",
    "evidence": "611.2152",
    "conclusion": "Requirement met",
    "readouts": [
      {
        "label": "Original capacity using flight speed",
        "expression": "0.5*rho*V^2*S*c*dCm",
        "unit": "N m",
        "value": 4002.48
      },
      {
        "label": "Capacity using local elevator airspeed",
        "expression": "0.5*rho*(flowFactor*V)^2*S*c*dCm",
        "unit": "N m",
        "value": 1961.2151999999999
      },
      {
        "label": "Required moment",
        "expression": "1350",
        "unit": "N m",
        "value": 1350
      },
      {
        "label": "Adjusted margin",
        "expression": "0.5*rho*(flowFactor*V)^2*S*c*dCm-1350",
        "unit": "N m",
        "value": 611.2151999999999
      }
    ],
    "inputs": {
      "flowFactor": 0.7
    }
  }
}

## Interpretation attempts
{
  "1": [
    {
      "correct": true,
      "feedback": "Your recorded value and choice match the calculation: Requirement met. Adjusted margin: 2,652.48 N m. 2,652.48 > 0 Your instructor will review your explanation.",
      "attemptId": "d64ef73e-3a62-4216-b9cc-4bed5e870a1b",
      "at": "2026-09-13T08:10:41.865Z",
      "conclusion": "Requirement met",
      "evidence": "2652.48",
      "note": "At a local speed factor of 1, the local airspeed equals the freestream speed exactly, so the adjusted capacity (4,002.48 N m) is identical to the original capacity — no reduction occurs.",
      "draftSnapshot": "{\"evidence\":\"2652.48\",\"conclusion\":\"Requirement met\",\"note\":\"At a local speed factor of 1, the local airspeed equals the freestream speed exactly, so the adjusted capacity (4,002.48 N m) is identical to the original capacity — no reduction occurs.\"}"
    }
  ],
  "0.5": [
    {
      "correct": true,
      "feedback": "Your recorded value and choice match the calculation: Insufficient authority. Adjusted margin: -349.38 N m. -349.38 < 0 Your instructor will review your explanation.",
      "attemptId": "d64ef73e-3a62-4216-b9cc-4bed5e870a1b",
      "at": "2026-09-13T08:14:52.820Z",
      "conclusion": "Insufficient authority",
      "evidence": "-349.38",
      "note": "At a local speed factor of 0.7, the local airspeed is 70% of freestream speed, so the adjusted capacity drops to 1,961.2152 N m — only 0.49 (0.7²) of the original 4,002.48 N m capacity, since moment scales with the square of speed.",
      "draftSnapshot": "{\"evidence\":\"-349.38\",\"conclusion\":\"Insufficient authority\",\"note\":\"At a local speed factor of 0.7, the local airspeed is 70% of freestream speed, so the adjusted capacity drops to 1,961.2152 N m — only 0.49 (0.7²) of the original 4,002.48 N m capacity, since moment scales with the square of speed.\"}"
    },
    {
      "correct": true,
      "feedback": "Your recorded value and choice match the calculation: Insufficient authority. Adjusted margin: -349.38 N m. -349.38 < 0 Your instructor will review your explanation.",
      "attemptId": "d64ef73e-3a62-4216-b9cc-4bed5e870a1b",
      "at": "2026-09-13T08:15:35.386Z",
      "conclusion": "Insufficient authority",
      "evidence": "-349.38",
      "note": "At a local speed factor of 0.5, the local airspeed is only half of freestream speed, so the adjusted capacity drops to 1,000.62 N m — just 0.25 (0.5²) of the original capacity. This is now below the 1,350 N m required moment, giving an adjusted margin of −349.38 N m.",
      "draftSnapshot": "{\"evidence\":\"-349.38\",\"conclusion\":\"Insufficient authority\",\"note\":\"At a local speed factor of 0.5, the local airspeed is only half of freestream speed, so the adjusted capacity drops to 1,000.62 N m — just 0.25 (0.5²) of the original capacity. This is now below the 1,350 N m required moment, giving an adjusted margin of −349.38 N m.\"}"
    }
  ],
  "0.7": [
    {
      "correct": true,
      "feedback": "Your recorded value and choice match the calculation: Requirement met. Adjusted margin: 611.2152 N m. 611.2152 > 0 Your instructor will review your explanation.",
      "attemptId": "d64ef73e-3a62-4216-b9cc-4bed5e870a1b",
      "at": "2026-09-13T08:15:04.705Z",
      "conclusion": "Requirement met",
      "evidence": "611.2152",
      "note": "At a local speed factor of 0.7, the local airspeed is 70% of freestream speed, so the adjusted capacity drops to 1,961.2152 N m — only 0.49 (0.7²) of the original 4,002.48 N m capacity, since moment scales with the square of speed.",
      "draftSnapshot": "{\"evidence\":\"611.2152\",\"conclusion\":\"Requirement met\",\"note\":\"At a local speed factor of 0.7, the local airspeed is 70% of freestream speed, so the adjusted capacity drops to 1,961.2152 N m — only 0.49 (0.7²) of the original 4,002.48 N m capacity, since moment scales with the square of speed.\"}"
    }
  ]
}

## Evidence status
Written reasoning awaits instructor review. This export is the current draft; compare it with the answer snapshot of the last run.

## Student reflection
Question: If disturbed flow changes both local speed and control effectiveness, what additional evidence would you need to revise the available-moment estimate?

Included: The experiment changes local speed at the control surface while holding the usable coefficient increment fixed.

Omitted: It does not model how disturbed flow might also change control effectiveness.

confirmedFor: d64ef73e-3a62-4216-b9cc-4bed5e870a1b

result: supported

observation: At factor 1, capacity was 4,002.48 N·m, margin 2,652.48 Nm. At factor 0.7, capacity was 1,961.2152 Nm, margin 611.2152 Nm. At factor 0.5, capacity 1,000.62, margin -349.38 Nm — insufficient. The claim fails somewhere between 0.7 and 0.5."

change: I confirmed that the freestream-based capacity estimate cannot be safely reused once local airspeed drops enough — the sufficient-authority claim held at factors 1 and 0.7, but failed at 0.5.

limit: I would need actual measured coefficient data (dCm) under disturbed flow conditions, since this experiment only varied speed while holding dCm fixed. If disturbed flow also reduces control effectiveness itself, the real available moment could be even lower than this speed-only model predicts