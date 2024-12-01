#include <iostream>
#include <vector>
#include <string>
#include <tuple>
#include <unordered_map>

class LZ77 {
public:
    LZ77(int window_size) : window_size(window_size) {}

    std::vector<std::tuple<int, int, char>> encode(const std::string& input) {
        std::vector<std::tuple<int, int, char>> encoded_output;
        int i = 0;
        int n = input.length();
        
        if (n == 0) return encoded_output;

        while (i < n) {
            int match_len = 0;
            int match_dist = 0;

            int window_start = std::max(0, i - window_size);
            for (int j = window_start; j < i; ++j) {
                int k = 0;
                while (k < window_size && (i + k) < n && input[j + k] == input[i + k]) {
                    ++k;
                }

                if (k > match_len) {
                    match_len = k;
                    match_dist = i - j;
                }
            }

            if (match_len == 0) {
                encoded_output.push_back(std::make_tuple(0, 0, input[i]));
                ++i;
            } else {
                encoded_output.push_back(std::make_tuple(match_dist, match_len, input[i + match_len]));
                i += match_len + 1;
            }
        }

        return encoded_output;
    }

    void decode(const std::vector<std::tuple<int, int, char>>& encoded) {
        std::string decoded_string;

        for (const auto& [dist, len, ch] : encoded) {
            if (dist == 0 && len == 0) {
                decoded_string.push_back(ch);
            } else {
                int start = decoded_string.length() - dist;
                for (int i = 0; i < len; ++i) {
                    decoded_string.push_back(decoded_string[start + i]);
                }
                decoded_string.push_back(ch);
            }
        }
        std::cout << "Decoded String: " << decoded_string << std::endl;
    }

private:
    int window_size;
};

int main() {
    LZ77 lz77(6);
    std::string input = "ABABABABACABA";
    
    if (input.empty()) {
        std::cout << "Input String is empty!" << std::endl;
        return 0;
    }
    
    std::cout << "Input String: " << input << std::endl;

    auto encoded = lz77.encode(input);

    std::cout << "Encoded Output:" << std::endl;
    for (const auto& [dist, len, ch] : encoded) {
        std::cout << "(" << dist << ", " << len << ", '" << ch << "') ";
    }
    std::cout << std::endl;

    lz77.decode(encoded);

    return 0;
}
