import string


# Function to remove punctuation and convert text into lowercase
def clean_text(text):
    text = text.lower()

    for ch in string.punctuation:
        text = text.replace(ch, "")

    return text


# Function to count sentences
def count_sentences(text):
    count = 0

    for ch in text:
        if ch in ".!?":
            count += 1

    if count == 0 and text.strip() != "":
        count = 1

    return count


# Function to analyse text
def analyze_text(text):

    if text.strip() == "":
        print("No text to analyse.")
        return

    cleaned_text = clean_text(text)

    words = cleaned_text.split()

    # Count words
    total_words = len(words)

    # Count characters including spaces
    total_characters = len(text)

    # Count sentences
    total_sentences = count_sentences(text)

    # Find unique words using set
    unique_words = set(words)

    # Count frequency using dictionary
    frequency = {}

    for word in words:
        if word in frequency:
            frequency[word] += 1
        else:
            frequency[word] = 1

    # Display results
    print("\n----- TEXT ANALYSIS -----")

    print("Total Words:", total_words)
    print("Total Characters:", total_characters)
    print("Total Sentences:", total_sentences)
    print("Unique Words:", len(unique_words))

    print("\nWord Frequency:")

    sorted_words = sorted(
        frequency.items(),
        key=lambda x: (-x[1], x[0])
    )

    for word, count in sorted_words:
        print(word, ":", count)

    print("\nTop 3 Words:")

    for word, count in sorted_words[:3]:
        print(word, ":", count)


# Function to read text from file
def read_file():

    filename = input("Enter file name: ")

    try:
        with open(filename, "r", encoding="utf-8") as file:
            text = file.read()

        analyze_text(text)

    except FileNotFoundError:
        print("File not found.")


# Main menu
def main():

    while True:

        print("\n===== WORD COUNTER & TEXT ANALYZER =====")
        print("1. Enter Text and Analyse")
        print("2. Word Frequency")
        print("3. Read Text From File")
        print("4. Exit")

        choice = input("Enter your choice: ")

        if choice == "1":

            text = input("Enter your text: ")
            analyze_text(text)

        elif choice == "2":

            text = input("Enter your text: ")

            if text.strip() == "":
                print("No text to analyse.")
                continue

            cleaned_text = clean_text(text)
            words = cleaned_text.split()

            frequency = {}

            for word in words:
                frequency[word] = frequency.get(word, 0) + 1

            sorted_words = sorted(
                frequency.items(),
                key=lambda x: (-x[1], x[0])
            )

            print("\nTop Words:")

            for word, count in sorted_words[:3]:
                print(word, ":", count)

            print("Unique Words:", len(set(words)))

        elif choice == "3":

            read_file()

        elif choice == "4":

            print("Thank you for using the project!")
            break

        else:

            print("Invalid choice! Please try again.")


# Start program
if __name__ == "__main__":
    main()# python-1
