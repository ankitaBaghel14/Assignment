# Assignment

#python assignment
import argparse
import string
from collections import Counter

def analyze_file(file_path):
    with open(file_path, 'r') as file:
        text = file.read()
    
  # Remove punctuation and convert to lowercase
  text = text.translate(str.maketrans('', '', string.punctuation)).lower()
    
  # Split into words and sentences
  words = text.split()
  sentences = text.split('.')
    
  # Stop words to ignore
  stop_words = {"the", "is", "and", "a", "an", "of", "in", "to", "it", "that"}
    
  # Filter out stop words
  filtered_words = [word for word in words if word not in stop_words]
    
  # Word count
  total_words = len(filtered_words)
    
  # Top 5 frequent words
  word_counts = Counter(filtered_words)
  top_5_words = word_counts.most_common(5)
    
  # Average word length
  avg_word_length = sum(len(word) for word in filtered_words) / total_words if total_words > 0 else 0
    
  # Number of sentences
  num_sentences = len([sentence for sentence in sentences if sentence.strip()])
    
  return {
        "Total Words": total_words,
        "Top 5 Frequent Words": top_5_words,
        "Average Word Length": avg_word_length,
        "Number of Sentences": num_sentences
    }

def main():
    parser = argparse.ArgumentParser(description="File Analyzer CLI Tool")
    parser.add_argument('file_path', type=str, help="Path to the text file to analyze")
    args = parser.parse_args()
    
  result = analyze_file(args.file_path)
    print("Analysis Report:")
    for key, value in result.items():
        print(f"{key}: {value}")

if __name__ == "__main__":
    main()
