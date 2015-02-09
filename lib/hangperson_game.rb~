class HangpersonGame

  # add the necessary class methods, attributes, etc. here
  # to make the tests in spec/hangperson_game_spec.rb pass.

 
	attr_accessor :guesses
	attr_accessor :wrong_guesses
	attr_accessor :word
	
	def initialize(nWord)
		@word = nWord
		@guesses = ''
		@wrong_guesses = ''
	end

	# Get a word from remote "random word" service
  def self.get_random_word
    require 'uri'
    require 'net/http'
    uri = URI('http://watchout4snakes.com/wo4snakes/Random/RandomWord')
    Net::HTTP.post_form(uri ,{}).body
  end
		
	def word_with_guesses
		space = ''
		word.each_char do|x|
			if @guesses.include? x
				space << x
			else
				space << '-'
			end
		end
		return space
	end

	def guess(letter)
		if (letter.nil? or !(letter =~ /^[[:alpha:]]$/))
			raise ArgumentError	
		end
		letter.downcase
		if @word.include? letter
			if @guesses.include? letter
				return false
			else
				@guesses += letter
			end
		else
			if @wrong_guesses.include? letter
				return false
			else
				@wrong_guesses += letter
			end
		end
	end

	def check_win_or_lose
		if wrong_guesses.length >= 7
			return :lose
		end
		word.each_char do|x|
			if !@guesses.include? x
				return :play
			end
		end
		return :win
	end
end
