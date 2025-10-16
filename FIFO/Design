module FIFO #(parameter width=8,length=8) 
  (input clk,reset,rd_req,wr_req,
   input [width-1:0]data_in,
   output full,empty,
   output reg [width-1:0]data_out);

  reg [$clog2(length)-1:0] rd_ptr,wr_ptr;
  reg [$clog2(length):0]count;
  reg [width-1:0]memory[length-1:0];

  always@(posedge clk)begin
    if(reset)begin  
      for (integer i=0;i<length;i=i+1) memory[i]<=0;                         
      count<=3'd0;
      data_out<=8'd0;
      rd_ptr<=3'd0;
      wr_ptr<=3'd0;
    end
    else begin
      if(wr_req && !full)begin
        memory[wr_ptr]<=data_in;
        if (wr_ptr==length-1) wr_ptr<=0;
        else wr_ptr<=wr_ptr+1;
        count<=count+1;
      end

      if(rd_req && !empty)begin
        data_out<=memory[rd_ptr];
        if (rd_ptr==length-1) rd_ptr<=0;
        else rd_ptr<=rd_ptr+1;
        count<=count-1;
      end
    end
  end
  assign full=(count==length);
  assign empty=(count==4'd0);
endmodule
