# computer_portfolio
import time
import random
import threading

# 알림 메시지 목록
alerts = [
    "잠시 일어나서 스트레칭을 하세요.",
    "간단한 몸 동작을 하여 혈액 순환을 촉진하세요.",
    "자주 눈을 깜박여서 눈의 피로를 줄이세요.",
    "잠깐 걸어서 산책을 하세요."
]

# 퀴즈 목록
quizzes = [
    ("1 + 1 = ?", "2"),
    ("5 - 3 = ?", "2"),
    ("3 * 3 = ?", "9"),
    ("8 / 2 = ?", "4"),
    ("12 + 15 = ?", "27"),
    ("7 * 6 = ?", "42"),
    ("(9 + 3) / 4 = ?", "3"),
    ("16 - (2 * 5) = ?", "6"),
    ("8 / (2 + 2) = ?", "2"),
    ("5 * (2 + 3) = ?", "25"),
    ("(3 + 4) * (5 - 2) = ?", "21"),
    ("30 / 5 = ?", "6"),
    ("(10 + 2) * 3 = ?", "36"),
    ("50 - 8 * 5 = ?", "10")
]

def show_alert():
    alert = random.choice(alerts)
    print(f"\n⚠️ 알림: {alert}")

def give_quiz():
    question, correct_answer = random.choice(quizzes)
    print(f"\n퀴즈: {question}")

    # 사용자 입력을 위한 타이머
    timer = threading.Timer(30.0, timeout)  # 30초 타이머 설정
    timer.start()

    try:
        user_answer = input("정답을 입력하세요: ")
        timer.cancel()  # 사용자가 답을 입력하면 타이머 취소
        if user_answer.strip() != correct_answer:
            print("정답이 틀렸습니다.")
            show_alert()
        else:
            print("정답입니다!")
    except KeyboardInterrupt:
        print("\n프로그램이 종료되었습니다.")
        timer.cancel()  # 프로그램이 종료되면 타이머 취소

def timeout():
    print("\n⏳ 시간이 초과되었습니다.")
    show_alert()

def main():
    print("졸음 방지 프로그램을 시작합니다. 프로그램이 실행되는 동안 퀴즈가 주기적으로 표시됩니다.")
    try:
        while True:
            give_quiz()
            print("5분 후에 다시 퀴즈가 제공됩니다.")
            time.sleep(300)  # 5분 (300초) 대기
    except KeyboardInterrupt:
        print("\n프로그램이 종료되었습니다.")

if __name__ == "__main__":
    main()
