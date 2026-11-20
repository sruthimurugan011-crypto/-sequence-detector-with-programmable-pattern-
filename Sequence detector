
module sequence_detector (
    input wire clk,
    input wire rst,
    input wire load_pattern,
    input wire [3:0] pattern_in,
    input wire serial_in,
    output reg detect
);

    reg [3:0] pattern_reg;
    reg [3:0] shift_reg;
    reg pattern_valid;

    wire [3:0] next_shift;

    assign next_shift = {shift_reg[2:0], serial_in};

    always @(posedge clk) begin
        if (rst) begin
            pattern_reg <= 4'b0000;
            shift_reg <= 4'b0000;
            pattern_valid <= 1'b0;
            detect <= 1'b0;
        end
        else begin
            detect <= 1'b0;

            if (load_pattern) begin
                pattern_reg <= pattern_in;
                pattern_valid <= 1'b1;
            end
            else begin
                shift_reg <= next_shift;

                if (pattern_valid &&
                    next_shift == pattern_reg) begin
                    detect <= 1'b1;
                end
            end
        end
    end

endmodule
