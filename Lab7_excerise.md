# Lab 7 - Multi-Agent Systems

## Exercise 1: Run and Understand

AutoGen and CrewAI demonstrate two fundamentally different multi-agent coordination styles.

In AutoGen, agents communicate through a shared GroupChat, where the GroupChatManager dynamically selects the next speaker. The workflow is conversational and iterative, with agents building on each other's ideas. For example, the AnalysisAgent referenced the ResearchAgent's findings, and the BlueprintAgent used those insights to design the product. The final output resembles a collaborative discussion.

In contrast, CrewAI follows a structured, sequential pipeline. Each agent is assigned a specific task, such as flight research, hotel selection, itinerary planning, and budget calculation. The output from each step is passed to the next agent without direct interaction between agents.

The CrewAI output clearly reflects this structure, producing a well-organized final report with sections such as flights, accommodation, activities, and budget.

Overall, AutoGen represents a dynamic, conversational system with emergent coordination, while CrewAI represents a structured, task-based workflow with predefined execution order.

---

## Exercise 2: Modify Agent Behavior

In this exercise, I modified the FlightAgent in CrewAI by updating its backstory to prioritize the cheapest flights over comfort or convenience.

After rerunning the system, the flight recommendations shifted toward lower-cost options, including budget airlines. For example, the system selected lower-priced flights from budget carriers rather than more expensive options, reducing the overall trip cost in the final budget output.

This demonstrates that in CrewAI, modifying a single agent directly affects downstream outputs, since the system follows a sequential pipeline: changes to the FlightAgent influence subsequent agents, such as the BudgetAgent.

In contrast, AutoGen would reflect such changes through dynamic conversation rather than a fixed pipeline.

---

## Exercise 3: Add a Fifth Agent

In this exercise, I extended the CrewAI system by adding a new agent called the Local Expert.

This agent provides practical local travel tips, including cultural insights, safety advice, and useful recommendations for travelers.

To implement this:
- I created a new agent (`create_local_agent`)
- I created a corresponding task (`create_local_task`)
- I added both the agent and task to the Crew configuration
- I updated the execution sequence to include the Local Expert before the budgeting step

The updated task sequence is:
FlightAgent → HotelAgent → ItineraryAgent → LocalExpertAgent → BudgetAgent

After integrating the new agent, I successfully ran the system and verified that the workflow executed correctly with five agents.

This demonstrates that CrewAI is easily extensible, enabling new agents to be added to the pipeline without modifying the overall architecture.

---

## Reflection

This lab helped me understand the differences between conversational and task-based multi-agent systems.

AutoGen enables flexible, interactive collaboration among agents, making it suitable for open-ended problem-solving. CrewAI, on the other hand, provides a structured, predictable workflow, making it better suited to pipeline-style tasks.

Additionally, modifying agent behavior and adding new agents demonstrated that multi-agent systems can be customized and extended to meet application needs.

During execution, I also observed occasional tool-calling errors, but the system recovered and continued, highlighting practical limitations of LLM-based systems.
