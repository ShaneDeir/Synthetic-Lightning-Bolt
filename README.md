# Welcome to my Synthetic Lightning Bolt!

This python script uses a continuous-time Markov chain to simulate a lightning bolt across 5 states for 10 seconds and graphs the results. 

The states are as follows:

 1. Forming
 2. Moving
 3. Splitting
 4. Striking
 5. Discharging

The state changes are calculated within a probability matrix. The following is a breakdown of the code step-by-step. 

    import numpy as np
    import matplotlib.pyplot as plt
These two lines import the necessary libraries for the script. `numpy` is used for numerical computations, and `matplotlib.pyplot` is used for plotting the results.

    # Set up the transition matrix
	   transition_matrix = np.array([[-0.9, 0.1, 0, 0, 0],  # from forming to forming, moving, splitting, striking, discharging
                              [0, -0.9, 0.1, 0, 0],  # from moving to forming, moving, splitting, striking, discharging
                              [0, 0, -0.9, 0.1, 0],  # from splitting to forming, moving, splitting, striking, discharging
                              [0, 0, 0, -0.9, 0.1],  # from striking to forming, moving, splitting, striking, discharging
                              [0, 0, 0, 0, 0]])  # from discharging to all states

This code sets up the transition matrix for the continuous-time Markov chain. The matrix has 5 rows and 5 columns, corresponding to the 5 states of the lightning bolt: "forming", "moving", "splitting", "striking", and "discharging".

The values in the matrix represent the probabilities of transitioning from one state to another. For example, the value in the first row and second column of the matrix is 1, which means that there is a probability of 1 of transitioning from the "forming" state to the "moving" state. Similarly, the value in the second row and third column of the matrix is 1, which means that there is a probability of 1 of transitioning from the "moving" state to the "splitting" state.

    # Set up the initial probabilities
	initial_probabilities = np.array([1, 0, 0, 0, 0])  # starts in the forming state

This code sets up the initial probabilities for the states of the lightning bolt. In this case, the initial probability is set to 1 for the "forming" state and 0 for all other states, which means that the lightning bolt starts in the "forming" state.

    # Set up the time steps
	time_steps = np.linspace(0, 10, 101)
	
This code sets up the time steps for the simulation. `np.linspace` is used to create an array of equally spaced values between 0 and 10 (the start and end times of the simulation), with a total of 101 values (including the start and end times). You can adjust the time step numbers to change how long your lightning bolt lasts for and compare the results. 

    # Calculate the probabilities at each time step
	probabilities = []
	for t in time_steps:
    probabilities.append(initial_probabilities @ np.linalg.matrix_power(transition_matrix, int(t / 0.1)))

Calculate the probabilities at each time step. This is done by looping through each time step and calculating the probabilities using matrix exponentiation. Matrix exponentiation is a mathematical operation that raises a matrix to a power. In this case, the matrix being exponentiated is the transition matrix, and the power is the time step divided by 0.1 seconds. This is done because the transition matrix represents the probabilities of transitioning from one state to another over a period of 0.1 seconds. By raising the transition matrix to the power of the time step divided by 0.1 seconds, we can calculate the probabilities of transitioning from one state to another over the desired time period. The probabilities are then appended to a list called `probabilities`.

    # Extract the probabilities of each state
	forming_probabilities = [p[0] for p in probabilities]
	moving_probabilities = [p[1] for p in probabilities]
	splitting_probabilities = [p[2] for p in probabilities]
	striking_probabilities = [p[3] for p in probabilities]
	discharging_probabilities = [p[4] for p in probabilities]

Extract the probabilities of each state. This is done by creating separate lists for the probabilities of each state, and extracting the corresponding probability from each element in the `probabilities` list.

    # Plot the results
	plt.plot(time_steps, forming_probabilities, label="Forming")
	plt.plot(time_steps, moving_probabilities, label="Moving")
	plt.plot(time_steps, splitting_probabilities, label="Splitting")
	plt.plot(time_steps, striking_probabilities, label="Striking")
	plt.plot(time_steps, discharging_probabilities, label="Discharging")
	plt.xlabel("Time (s)")
	plt.ylabel("Probability")
	plt.legend()
	plt.ylim(0, 1)  # set the y-axis limits to 0-100%
	plt.yticks(np.arange(0, 1.1, 0.1))  # set the y-axis tick marks to 0%, 10%, ..., 100%
	plt.grid()  # show a grid
	plt.show()

This plots our synthetic lightning bolt into a graph so we can visually analyze the results. I hope you enjoyed the journey! Thank you and congratulations for making it this far! 
