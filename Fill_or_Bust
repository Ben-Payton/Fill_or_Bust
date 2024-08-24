import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt

class player:
	
	def __init__(self):
		self.remaining_die = 6
		self.held_die = []
		self.score = 0
		
	def calc_score(self, die_list) -> int:
		current_total = 0
		die_counts = { 1 : 0,
								  2 : 0,
								  3 : 0,
								  4 : 0,
								  5 : 0,
								  6 : 0}
		for die in die_list:
			die_counts[die] = die_counts[die] + 1
		while die_counts[1] > 0:
			if die_counts[1] >= 3:
				die_counts[1] = die_counts[1] - 3
				current_total = current_total + 1000
			else:
				die_counts[1] = die_counts[1] - 1
				current_total = current_total + 100
		while die_counts[5] > 0:
			if die_counts[5] >= 3:
				die_counts[5] = die_counts[5] - 3
				current_total = current_total + 500
			else:
				die_counts[5] = die_counts[5] - 1
				current_total = current_total + 50
				
		for option in [2,3,4,6]:
			while die_counts[option] == 3 or die_counts[option] == 6:
				die_counts[option] = die_counts[option] - 3
				current_total = current_total + option * 100
		return current_total

	def roll(self):				
		x = np.random.randint(1,7,self.remaining_die)
		return x
		
	def bust(self):
		self.remaining_die = 6
		self.held_die = []
		return 0
		
	def add_hand_to_score(self):
		self.score = self.calc_score(self.held_die) + self.score
		return self.score
	
	def present_options(self,die_list):
		die_counts = { 1 : 0,
								  2 : 0,
								  3 : 0,
								  4 : 0,
								  5 : 0,
								  6 : 0}
		for die in die_list:
			die_counts[die] = die_counts[die] +1
		for option in [2,3,4,6]:
			die_counts[option] = (die_counts[option] // 3) * 3
		return die_counts		
		
	def strat_take_all_till_bust(self):
				bust = 1
				while bust == 1 and self.remaining_die > 0:
					current_roll = self.roll()
					if self.calc_score(current_roll) == 0:
						bust = self.bust()
						break
					else: 
						po = self.present_options(current_roll)
						for option in po:
							for occ in range(po[option]):
								self.held_die.append(option)
						self.remaining_die = 6 - len(self.held_die)
				self.add_hand_to_score()
				return self.score
					
					
				
def main():
	
	x = []
	for i in range(500000):
		n = 0
		player1 = player()
		
		while player1.score < 10000:
			n = n +1
			player1.strat_take_all_till_bust()
			
		x.append(n)
		
	g = np.array(x)
	del x
	
	print("mean",g.mean())
	print("std",g.std())
	
	sns.histplot(g,kde=True)
	plt.show()
	
	
	

main()
