module password_lock (
    input  [3:0] key,
    input        key_strobe,
    output reg   locked_led,
    output reg   unlock_led,
    output reg   error_led
);

    parameter [3:0] PASSWORD = 4'b1010;

    always @(*) begin
        // Default state
        locked_led = 1;
        unlock_led = 0;
        error_led  = 0;

        if (key_strobe) begin
            if (key == PASSWORD) begin
                unlock_led = 1;
                locked_led = 0;
                error_led  = 0;
            end
            else begin
                error_led  = 1;
                locked_led = 1;
                unlock_led = 0;
            end
        end
    end

endmodule

