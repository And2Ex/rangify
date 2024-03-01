def rangify_input(data_input, delete_slashes_input=True):
    if isinstance(data_input, str):
        data_string = data_input.lstrip('буд.').lstrip('Буд.').rstrip(',').replace('.', ',')
        # "буд." and "Буд." represent the abbreviation for "building". You can replace it with your own term.
    elif isinstance(data_input, list):
        data_string = ",".join(map(str, data_input))
    else:
        raise ValueError("Input data must be a string or a list")

    # Deleting slashes and everything after them if it's a number
    if delete_slashes_input:
        data_string = ",".join(part.split("/")[0] if "/" in part and part.split("/")[0].isdigit()
                               else part for part in data_string.split(","))

    # Splitting ranges
    if '-' in data_string:
        split_values = data_string.split(',')
        result_list = []

        for value in split_values:
            if '-' in value:
                ranges = value.split('-')
                if all(sub_value.isdigit() or '-' in sub_value for sub_value in ranges):
                    start, end = map(str, [ranges[0], ranges[-1]])
                    result_list.extend(str(x) for x in range(int(start), int(end) + 1))
                else:
                    result_list.append(value)
            else:
                result_list.append(value)

        data_string = ",".join(result_list)

    # If more than one value
    if ',' in data_string:
        data_list = data_string.split(',')

        number_list = sorted(
            set(int(x) for x in data_list if x and (x.isdigit() or '-' in x and x.replace('-', '').isdigit())))
        non_number_list = sorted(
            set(x for x in data_list if x and not (x.isdigit() or '-' in x and x.replace('-', '').isdigit())))

        result_string = ""

        if number_list:
            start_range = number_list[0]
            end_range = start_range

            for num in number_list[1:]:
                if num == end_range + 1:
                    end_range = num
                else:
                    if start_range == end_range:
                        result_string += f"{start_range},"
                    else:
                        result_string += f"{start_range}-{end_range},"

                    start_range = end_range = num

            if start_range == end_range:
                result_string += f"{start_range}"
            else:
                result_string += f"{start_range}-{end_range}"

            if non_number_list:
                result_string += "," + ",".join(non_number_list)

        elif non_number_list:
            result_string = ",".join(non_number_list)

        return result_string

    else:
        return data_string


if __name__ == '__main__':
    delete_slashes = False
    while True:
        test_string = '1,2,2B,3,5,4,6,9,10-12-15,22,55,77,78,1,3,21,24,23,26,27.28,5/74'
        input_string = (input(f"Enter string (Enter - test, q - exit, i - info, "
                              f"/ - {'not ' if delete_slashes else ''}delete slashes and numbers after them):\n")
                        .lstrip('буд.').lstrip('Буд.')
                        .rstrip(',')
                        .replace('.', ',')
                        or test_string)

        if input_string.lower() == 'q':
            break
        if input_string == '/':
            delete_slashes = False if delete_slashes else True
            continue
        if input_string.lower() == 'i':
            print('1. Remove "буд." from the beginning of the string if present.\n'
                  '2. Remove comma from the end of the string if present.\n'
                  '3. Use comma and dot as delimiters.\n'
                  '4. If ranges already exist, split them by hyphen '
                  '   (including non-numeric values like "1-B").\n'
                  '5. Remove all duplicates.\n'
                  '6. Generate ranges from integer values.\n'
                  '7. Sort all values: numeric ones first, then others.\n')
            continue

        print()
        print("Input string:", input_string)

        formatted_string = rangify_input(input_string, delete_slashes)

        print("Output string:", formatted_string)
        print()
