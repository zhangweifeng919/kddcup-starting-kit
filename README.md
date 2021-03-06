# The Starting Kit for Learning to Dispatch and Reposition Competition

This repository is the official Learning to Dispatch and Reposition (LDR) Competition **submission template and starter kit**! Clone this to make a new submission!

![](http://img-hxy021.didistatic.com/static/outreach/KDD_Cup_1000X500_2020-3-30.jpg)

**Other Resources**:
- [DiDi Official Announcement](https://outreach.didichuxing.com/competition/kddcup2020/) - Background and overview.
- [LDR Competition Page](https://biendata.com/competition/kdd_didi/) - Main registration page & leaderboard
- [GAIA Open Dataset](https://outreach.didichuxing.com/research/opendata/en/) - Download the competition dataset

**Contact**

Please contact the organizers (kddcup2020@didiglobal.com) if you have any problem concerning this challenge.


```
.
├── samples                 # The sample data illustrating the api of your agent required by the simulator.
├── local_test.py           # A demo of how your agent will be used during simulation.
├── run_local.sh            # Run test in the simulation environment.
├── environment.yml         # The simulation environment specified in a conda environment file.
├── Dockerfile              # The simulation environment specified in a Dockerfile.
├── README                  # The readme file.
└── model                   # IMPORTANT: Your submission folder.
    └── agent.py            # IMPORTANT: Your implementation of the dispatch and reposition.
```

## Quick Start

Clone this repo. Create your submission bundle by zipping the whole `model` folder. Make sure no extra directories are created within the zip, e.g., `zip -j submission.zip model/*`. And head over to the [competition website](https://biendata.com/competition/kdd_didi/) for your first submission!

## Implement your own dispatch and reposition agent!

A LDR agent is equipped with two performable actions, `dispatch` and `reposition`, which receive `observations` from the environment and compute order-driver assignment and repositioning destinations for the drivers.

```python
class Agent(object):
  """ Agent for dispatching and reposition """

  def __init__(self):
    """ Load your trained model and initialize the parameters """
    pass

  def dispatch(self, dispatch_observ):
    """ Compute the assignment between drivers and passengers at each time step
    :param dispatch_observ: a list of dict, the key in the dict includes:
        order_id, int
        driver_id, int
        order_driver_distance, float
        order_start_location, a list as [lng, lat], float
        order_finish_location, a list as [lng, lat], float
        driver_location, a list as [lng, lat], float
        timestamp, int
        order_finish_timestamp, int
        day_of_week, int
        reward_units, float
        pick_up_eta, float

    :return: a list of dict, the key in the dict includes:
        order_id and driver_id, the pair indicating the assignment
    """
    pass

  def reposition(self, repo_observ):
    """ Compute the reposition action for the given drivers
    :param repo_observ: a dict, the key in the dict includes:
        timestamp: int
        driver_info: a list of dict, the key in the dict includes:
            driver_id: driver_id of the idle driver in the treatment group, int
            grid_id: id of the grid the driver is located at, str
        day_of_week: int

    :return: a list of dict, the key in the dict includes:
        driver_id: corresponding to the driver_id in the od_list
        destination: id of the grid the driver is repositioned to, str
    """
    pass

```

Look into the `agent.py` file inside the `model` folder for more details. The `agent.py` implements a default policy and is provided for you to base your submission. The `model` folder should contain all your submitted files including your implementations and dependencies.

## Test your agent before submission

To make sure your agent run correctly in the online evaluation environment, you just need to run

```bash
./run_local.sh
```

It will launch a docker environment, import your model and call your agent on a sample dataset provided for you as a quick test before the submission.

In particular, the `local_test.py` gives an example of how your submission will be used in the simulation and the `Dockerfile` describes the environment where your `agent.py` will be executed.



