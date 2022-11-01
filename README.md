# DS-542-Week-7-Assignment

import pandas as pd 

def get_csv(web_link):
    df = pd.read_csv(web_link)
    return df
    
df = get_csv(r'https://raw.githubusercontent.com/odonnell31/NBA-Team-Strategies/main/data/nba_teams_data_1990_2020.csv')
  
df.head()

import matplotlib.pyplot as plt

knicks_data = df[df["Team"] == "Atlanta Hawks"]

knicks_data.head(11)

# Line Graph

x = knicks_data["Year"]
y = knicks_data["W"]

plt.plot(x,y)
plt.title("Atlanta Hawks Wins Over Time")
plt.xlabel("Year")
plt.ylabel("Wins")
plt.show()


playoff_data = df.groupby("Team")[["Playoffs", "Finals_Team"]].agg("sum")

# Bar Plot

playoff_data = playoff_data.sort_values(by = "Playoffs", ascending = False)

x = playoff_data.index
y = playoff_data["Playoffs"]

plt.figure(figsize = (10, 5))
plt.bar(x, y, color = "purple")
plt.xticks(rotation = "vertical")
plt.show()

# Histogram

plt.hist(knicks_data["W"], bins = 10)
plt.title("Knicks Wins Histogram")
plt.xlabel("Wins")
plt.ylabel("Number of Years")
plt.show()

# Violin Plot

plt.figure(figsize = (10, 3))
plt.violinplot(knicks_data["W"], vert = False,
               showextrema = True, showmeans = True)

plt.title("Knicks Wins Violin Plot")
plt.show()
