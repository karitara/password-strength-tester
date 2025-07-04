# password-strength-tester
import re 
import string
def test_password_strength(password):
    score=0
    feedback=[]

    if len(password) < 8 :
        feedback.append("Password is too short. Minimum 8 characters required.")
    elif len(password) >= 12:
        score += 2
        feedback.append("Good Length!")
    else:
       score += 1

    if re.search(r'[A-Z]' , password):
        score += 1
        feedback.append("Contains uppercase letters")
    else:
        feedback.append("Missing uppercase letters")

    if re.search(r'[a-z]' , password):
        score += 1
        feedback.append("contains lowercase letters")
    else:
        feedback.append("Missing lowercase letters")


    if re.search(r'\d', password):
        score +=1
        feedback.append("Contains numbers")
    else:
        feedback.append("Missing numbers")


    if re.search(r'[!@#$%^&*()<>?":{}|<>]' , password):
        score +=1
        feedback.append("contains special characters")
    else:
        feedback.append("Missing special characters")

    common_patterns = [
        '123456', 'password', 'qwerty', 'admin', 
        'letmein', 'welcome', '12345678'
    ]


    if any(pattern in password.lower() for pattern in common_patterns):
        score -= 2
        feedback.append("Contains common patterns - avoid these!")



    if score < 2:
        strength = "Very Weak"
    elif score < 3:
        strength = "Weak"
    elif score < 4:
        strength = "Moderate"
    elif score < 5:
        strength = "Strong"
    else:
        strength = "Very Strong"

    return {
        'strength': strength,
        'score': score,
        'feedback': feedback
    }


    def main():
    while True:
        password = input("\nEnter a password to test (or 'quit' to exit): ")
        if password.lower() == 'quit':
            break
            
        result = test_password_strength(password)
        
        print("\nPassword Strength Analysis:")
        print("-" * 25)
        print(f"Strength: {result['strength']}")
        print(f"Score: {result['score']}/6")
        print("\nFeedback:")
        for item in result['feedback']:
            print(f"- {item}")

if __name__ == "__main__":
    main()
    
