# DataWareHouse_Assn_2

Que.1] What are the strengths and weaknesses of each option?

Option A:

Strengths:
=> Maintains the intended grain of one row per student per course enrollment in the fact table.
=> Allows inclusion of the Instructor dimension in the fact table.
Enables analysis of instructor popularity and teams.
=> Provides a straightforward representation of instructor teams.

Weaknesses:
=> Introduces complexity in data management and reporting, especially for courses with multiple instructors.
=> May require additional processing to aggregate data from instructor teams in queries involving individual instructors.
=> Requires identification and handling of instructor teams separately, which can be time-consuming and error-prone.
=> Reporting and analysis involving individual instructors might be more challenging due to the presence of instructor teams.

Option B:

Strengths:
=> Includes the Instructor dimension in the fact table.
=> Allocates enrollments equally among multiple instructors, ensuring fairness in calculations.
=> Preserves the original grain of one row per student per course enrollment in the fact table.

Weaknesses:
=> Introduces fractional values (0.5) in the EnrollmentCount field, which can complicate queries and reporting.
=> May require additional calculations and considerations to aggregate fractional enrollments properly.
=> Reporting and analysis involving the Instructor dimension may require additional processing and interpretation of fractional enrollments.
=> Can potentially confuse users who are not familiar with the fractional allocation of enrollments.

Option C:

Strengths:
=> Separates concerns by having two fact tables, simplifying queries based on the specific requirements.
=> Provides a clear distinction between queries involving the Instructor dimension and other queries.
=> Enables efficient querying for attributes related to the Instructor dimension.

Weaknesses:
=> Requires managing and maintaining two fact tables, which can increase complexity and maintenance efforts.
=> May lead to duplicated data if the dimensions shared between the two fact tables are not synchronized properly.
=> Users need to be aware of which fact table to use for different types of queries, adding complexity to the system.
=> Might limit the flexibility of ad-hoc querying as users need to be aware of the division between the two fact tables.




Que.2] Which option would you choose and why?

 Option A (modifying the Instructor dimension by adding special rows representing instructor teams) seems like a reasonable choice in many cases. It allows for the inclusion of the Instructor dimension while maintaining the intended grain of one row per student per course enrollment. This option provides flexibility in analyzing instructor popularity and teams, and it does not introduce fractional values or require managing multiple fact tables like Options B and C.

However, it's important to carefully evaluate the requirements and potential challenges specific to your system before making a decision. Consider factors such as the frequency of courses with multiple instructors, the impact of complexity on data management and reporting, and the resources available for implementation and maintenance. It may also be beneficial to consult with stakeholders and experts in the field to gather different perspectives and make an informed decision based on the specific needs and constraints of your project.



Que.3] Would your answer to Question 2 be different if the majority of classes had multiple instructors? How about if only one or two classes had multiple instructors? (Explain your answer.)

=> If the majority of classes had multiple instructors, it would significantly impact the analysis and decision-making regarding the options. In such a scenario, Option A (modifying the Instructor dimension by adding special rows representing instructor teams) would become more appealing. Since multiple instructors are prevalent, Option A would align well with the data by allowing the representation of instructor teams and their popularity. It would also accommodate the majority of cases without introducing significant complexity or data management challenges.

On the other hand, if only one or two classes had multiple instructors while the majority had a single instructor, the impact on the analysis and decision-making would be different. In this case, Option A might still be a viable choice, especially if the classes with multiple instructors are significant in terms of enrollment or importance. By modifying the Instructor dimension to include special rows for instructor teams, Option A would accurately capture the information for those specific classes without overly complicating the majority of cases with single instructors.

However, if the classes with multiple instructors are rare and insignificant in terms of enrollment or importance, the impact of multiple instructors might not justify the complexity introduced by Option A. In such a scenario, it might be more efficient to consider a simpler approach, such as Option B (changing the grain of the fact table to one row per student enrollment per course per instructor with fractional enrollments). This approach would still allow for the inclusion of the Instructor dimension while maintaining a reasonable level of simplicity in data management and reporting.




Scenario II

Que. 5]  What are the strengths and weaknesses of each option?

Option A:

Strengths:
=> Simplifies the data model by storing the scores as attributes of the Customer dimension.
=> Allows for straightforward filtering and grouping based on the scores in queries.
=> Requires less storage space compared to other options.

Weaknesses:
=> Overwriting the old score with the new score (Type 1 Slowly Changing Dimension) does not preserve historical data and makes it challenging to track changes in customer scores over time.
=> Limited ability to analyze and understand how and why customer scores change.
=> May not capture the historical context of customer scores, potentially limiting the depth of analysis.

Option B:

Strengths:
=> Preserves historical data by creating new Customer dimension rows when scores change (Type 2 Slowly Changing Dimension).
=> Enables tracking changes in customer scores over time and understanding the evolution of activity and profitability levels.
=> Provides a comprehensive view of customer scores for analysis and reporting purposes.

Weaknesses:
=> Increases storage requirements due to the creation of new dimension rows.
=> Complexity in querying and reporting to accurately consider the appropriate customer score for each trade based on the trade date.
=> Requires additional effort to manage and maintain the dimension table with historical changes.

Option C:

Strengths:
=> Stores the scores in a separate CustomerScores dimension, providing a dedicated dimension for activity and profitability scores.
=> Allows for efficient filtering and grouping based on the scores using foreign key references.
=> Provides a fixed set of rows in the CustomerScores dimension, simplifying management and ensuring consistency.

Weaknesses:
=> Limited flexibility in handling changes to the scoring criteria or the addition of new scores beyond the predefined combinations.
=> Requires an additional join between the Trades fact table and the CustomerScores dimension for queries involving the scores.
=> Difficulty in understanding the historical changes in customer scores without proper tracking or versioning.

Option D:
Strengths:
=> Stores the scores in a CustomerScores outrigger table, providing a separate table for the scores without modifying the fact table.
=> Allows for efficient filtering and grouping based on the scores using foreign key references.
=> Provides a clear separation between the Customer dimension and the customer scores.

Weaknesses:
=> Requires updating the foreign key column in the Customer table to point to the correct outrigger row when scores change.
=> Potential complexity in managing and maintaining the outrigger table and ensuring data integrity.
=> Limited historical tracking and understanding of changes in customer scores without proper versioning or tracking mechanisms.



Que. 6]  Which option would you choose and why?


Option B (Type 2 Slowly Changing Dimension) seems to be the most suitable choice.

Here's why:

Preservation of historical data: Option B preserves historical data by creating new Customer dimension rows when scores change. This allows for tracking changes in customer scores over time and understanding the evolution of activity and profitability levels. It provides a comprehensive view of customer scores and enables analysis of how and why customer scores change.

Analysis and reporting capabilities: Option B allows for more in-depth analysis of customer scores by maintaining historical context. It enables queries that involve filtering and grouping based on specific customer scores at different points in time. This flexibility supports the use cases mentioned in the scenario, such as analyzing trades by profitability score and understanding changes in customer activity segments.

Flexibility and scalability: Option B accommodates changes in scoring criteria or the addition of new scores by creating new dimension rows. This ensures the ability to adapt the scoring system over time without compromising historical data or reporting capabilities.

Although Option B may require additional storage space compared to Option A, it offers the advantage of preserving historical data, providing a more detailed analysis of customer scores, and accommodating changes in the scoring system. However, it's important to assess the specific requirements, resources, and trade-offs involved before making a final decision.





Que. 7] Would your answer to Question 6 be different if the number of customers and/or the time interval between score recalculations was much larger or much smaller? (Explain your answer.)

=> Yes, the answer to Question 6 would be different if the number of customers and/or the time interval between score recalculations was much larger or much smaller.

If the number of customers is much larger, it would impact the storage requirements and performance considerations. Option B, which creates new dimension rows for each customer score change, could result in a significant increase in the size of the Customer dimension. This would require more storage space and potentially impact query performance. In such cases, Option A or Option C, which do not create additional dimension rows, might be more suitable to manage the data efficiently.

Conversely, if the number of customers is much smaller, the impact on storage and performance would be less pronounced. The differences between the options may become less significant, and the choice could be based more on the reporting and analysis requirements. Option B, with its ability to preserve historical data and track changes in customer scores, would still be advantageous for understanding the evolution of activity and profitability levels, even with a smaller number of customers.

Similarly, the time interval between score recalculations would also influence the choice of options. If the interval is much larger, the frequency of score changes would be lower, reducing the need for frequent updates to the dimension table. Option A or Option C might be more appropriate in such cases to simplify the data model and minimize maintenance efforts.

On the other hand, if the time interval is much smaller, resulting in frequent score recalculations, Option B could still be a suitable choice. It allows for capturing and preserving the historical context of customer scores, facilitating analysis of how scores change over time and providing valuable insights into customer behavior.

In summary, the number of customers and the time interval between score recalculations impact factors such as storage requirements, performance considerations, and the need for historical tracking. The choice of options should be evaluated based on these factors and the specific requirements and constraints of the data warehouse project.
