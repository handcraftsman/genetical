# genetical
Genetic Algorithm engine built in [Genetic Algorithms with Python](https://leanpub.com/genetic_algorithms_with_python)

## Example

	import datetime
	import genetical
	import unittest
	import random
    
    
	def get_fitness(guess, target):
		return sum(1 for expected, actual in zip(target, guess)
				   if expected == actual)
    
    
	def display(candidate, startTime):
		timeDiff = datetime.datetime.now() - startTime
		print("{0}\t{1}\t{2}".format(
			''.join(candidate.Genes),
			candidate.Fitness,
			str(timeDiff)))
    
    
	class GuessPasswordTests(unittest.TestCase):
		geneset = " abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ!.,"

		def test_Hello_World(self):
			target = "Hello World!"
			self.guess_password(target)

		def test_For_I_am_fearfully_and_wonderfully_made(self):
			target = "For I am fearfully and wonderfully made."
			self.guess_password(target)

		def guess_password(self, target):
			startTime = datetime.datetime.now()

			def fnGetFitness(genes):
				return get_fitness(genes, target)

			def fnDisplay(candidate):
				display(candidate, startTime)

			optimalFitness = len(target)
			best = genetical.get_best(fnGetFitness, len(target),
									  optimalFitness, self.geneset, fnDisplay)

			self.assertEqual(''.join(best.Genes), target)
    			
	if __name__ == '__main__':
		unittest.main()

## License

[Apache license 2.0](https://opensource.org/licenses/Apache-2.0)