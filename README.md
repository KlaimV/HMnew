def checker(*exc_types):
    def decorator(function):
        def wrapper(*args, **kwargs):
            try:
                result = function(*args, **kwargs)
                print(f"No problems. Result - {result}")
                return result
            except exc_types as exc:
                print(f"We encountered a problem: {exc}")

        return wrapper

    return decorator


@checker(NameError, TypeError, SyntaxError, ZeroDivisionError, ValueError)
def calculate(expression):
    expression = expression.replace(" ", "")

    allowed_chars = "0123456789+-*/()."
    for char in expression:
        if char not in allowed_chars:
            raise ValueError(f"Invalid character detected: {char}")

    return eval(expression)


calculate("2 + 12")  
calculate("2 / 0")
calculate("2 + ")
calculate("10 * (5 + 3)")
calculate("3 + 5 * abc")

