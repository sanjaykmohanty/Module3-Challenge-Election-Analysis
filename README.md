# Election Audit Analysis

## Overview 
Colorado Board of Elections conducted a local congressional election. The purpose of this project is to develop an audit report for the election results. 

The report outlines below listed information for the Colorado election commission.
1. Calculate the total number of votes cast.
2. The voter turnout for each county.
3. The percentage of votes from each county out of the total count.
4. The county with the highest turnout.
5. Get a complete list of candidates who received votes.
6. Calculate the total number of votes each candidate received.
7. Calculate the percentage of votes each candidate own.
8. Determine the winner of the election based on popular vote.

## Resources
Data Source: election_results.csv Software: Python 3.9.12, Visual Studio Code 1.71.0

## Results
The analysis of the election shows that:

- There are 369,711 votes cast in the election.
- The election was conducted in 3 counties: 
    - Jefferson
    - Denver
    - Arapahoe
- Denver county had the highest voter turnout
- Voter turnout for each county:
    - 38,855 votes from Jefferson County, 10.5% of the total votes came from this county
    - 306,055 votes from Denver County, 82.8% of the total votes came from this county
    - 24,801 votes from Arapahoe County, 6.7% of the total votes came from this county
- The candidates were:
    - Charles Casper Stockham
    - Diana DeGette
    - Raymon Anthony Doane
- The candidate results were:
    - Charles Casper Stockham received 23.0% of the vote and 85,213 number of votes.
    - Diana DeGette received 73.8% of the vote and 272,892 number of votes.
    - Raymon Anthony Doane received 3.1% of the votes and 11,606 number of votes.
- The winner of the election was:
    - Diana DeGette, who received 73.8% vote and 272,892 number of votes.

## Summary

The script developed to create the audit report uses election results data as input and to process the data to generate the required information. The election result file has following data points:
- Ballot ID - Unique ID for each voter 
- County - County name where election was conducted
- Candidate - Candidate marked in the ballot by the voter

The script developed to create the audit report uses election results data as input and process the data to generate the required information. The election result file has following data points:
- Ballot ID - Unique ID for each voter
- County - Name of the county 
- Candidate - Candidate marked in the ballot by the voter

The script has logic to scan through the election results data and produce an election analysis audit report as described under the result section of this document. Code used in the script is shown below.

### Python Code Used in Script

    # -*- coding: UTF-8 -*-
    """PyPoll Homework Challenge Solution."""

    # Add our dependencies.
    import csv
    import os

    # Add a variable to load a file from a path.
    file_to_load = os.path.join("Resources", "election_results.csv")
    # Add a variable to save the file to a path.
    file_to_save = os.path.join("Analysis", "election_analysis.txt")

    # Initialize a total vote counter.
    total_votes = 0

    # Candidate Options and candidate votes.
    candidate_options = []
    candidate_votes = {}

    # 1: Create a county list and county votes dictionary.
    county_list = []
    county_votes = {}


    # Track the winning candidate, vote count and percentage
    winning_candidate = ""
    winning_count = 0
    winning_percentage = 0

    # 2: Track the largest county and county voter turnout.
    largest_county = ""
    county_max_count = 0
    county_max_turnout = 0

    # Read the csv and convert it into a list of dictionaries
    with open(file_to_load) as election_data:
        reader = csv.reader(election_data)

        # Read the header
        header = next(reader)

        # For each row in the CSV file.
        for row in reader:

            # Add to the total vote count
            total_votes = total_votes + 1

            # Get the candidate name from each row.
            candidate_name = row[2]

            # 3: Extract the county name from each row.
            county_name = row[1]

            # If the candidate does not match any existing candidate add it to
            # the candidate list
            if candidate_name not in candidate_options:

                # Add the candidate name to the candidate list.
                candidate_options.append(candidate_name)

                # And begin tracking that candidate's voter count.
                candidate_votes[candidate_name] = 0

            # Add a vote to that candidate's count
            candidate_votes[candidate_name] += 1

            # 4a: Write an if statement that checks that the
            # county does not match any existing county in the county list.

            if county_name not in county_list:

                # 4b: Add the existing county to the list of counties.
                county_list.append(county_name)
        
                # 4c: Begin tracking the county's vote count.
                county_votes[county_name] = 0

            # 5: Add a vote to that county's vote count.
            county_votes[county_name] += 1


    # Save the results to our text file.
    with open(file_to_save, "w") as txt_file:

        # Print the final vote count (to terminal)
        election_results = (
            f"\nElection Results\n"
            f"-------------------------\n"
            f"Total Votes: {total_votes:,}\n"
            f"-------------------------\n\n"
            f"County Votes:\n")
    
        print(election_results, end="")

        txt_file.write(election_results)

        # 6a: Write a for loop to get the county from the county dictionary.
        for county_name in county_votes:
            # 6b: Retrieve the county vote count.
            c_votes = county_votes.get(county_name)
            # 6c: Calculate the percentage of votes for the county.
            c_vote_percentage = float(c_votes) / float(total_votes) * 100

            # 6d: Print the county results to the terminal.
            county_results = (
                f'{county_name}: {c_vote_percentage:.1f}% ({c_votes:,})\n')
            print(county_results)
            # 6e: Save the county votes to a text file.
            txt_file.write(county_results)
            # 6f: Write an if statement to determine the winning county and get its vote count.
            if (c_votes > county_max_count) and (c_vote_percentage > county_max_turnout):
                county_max_count = c_votes
                largest_county = county_name
                county_max_turnoute = c_vote_percentage

        # 7: Print the county with the largest turnout to the terminal.
        turnout_summary = (
            f"\n-------------------------\n"
            f"Largest County Turnout: {largest_county}\n"
            f"-------------------------\n")
        print(turnout_summary)
        # 8: Save the county with the largest turnout to a text file.
        txt_file.write(turnout_summary)

        # Save the final candidate vote count to the text file.
        for candidate_name in candidate_votes:

            # Retrieve vote count and percentage
            votes = candidate_votes.get(candidate_name)
            vote_percentage = float(votes) / float(total_votes) * 100
            candidate_results = (
                f"{candidate_name}: {vote_percentage:.1f}% ({votes:,})\n")

            # Print each candidate's voter count and percentage to the
            # terminal.
            print(candidate_results)
            #  Save the candidate results to our text file.
            txt_file.write(candidate_results)

            # Determine winning vote count, winning percentage, and candidate.
            if (votes > winning_count) and (vote_percentage > winning_percentage):
                winning_count = votes
                winning_candidate = candidate_name
                winning_percentage = vote_percentage

        # Print the winning candidate (to terminal)
        winning_candidate_summary = (
            f"-------------------------\n"
            f"Winner: {winning_candidate}\n"
            f"Winning Vote Count: {winning_count:,}\n"
            f"Winning Percentage: {winning_percentage:.1f}%\n"
            f"-------------------------\n")
        print(winning_candidate_summary)

        # Save the winning candidate's name to the text file
        txt_file.write(winning_candidate_summary)

### Usability of Script in Other Elections
This script was developed based on the requirements received from the Colorado election commission and can be used for election results analysis of any other local congressional election. If the audit requirement remains same, the script can be used with minor changes. Although the script satisfies most of the elction analysis audit requirements, if the audit requirement changes, the script can be modified to satisfy the requirement.

If the requirements remain same, the script can be used for other elction result analysis with below changes:
- Either the file name of the CSV file containg election data can be changed in the script or the file can be renamed 
- Based on the type of election, in addion to county level informaion, the script can be modified to include congressional district and state level information
