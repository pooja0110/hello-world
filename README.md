# hello-world
#calculating bond length from pdb file
open(F,"diala4.sd")or die "file not found";
open(G,"conntable.txt")or die "file not found";
%hash1=();
%hash2=();
%hash3=();

while (chomp($line =<F>))
{
if($line=~/(\S+)\s+(\S+)\s+(\S+)\s+(\d+)\s+\d\s+\d/)
{
#print"$1\t$2\t$3\t$4\t\n"; 
$hash1{$4} = $1;
$hash2{$4} = $2;
$hash3{$4} = $3;
}
}
while (chomp($conn=<G>))
{
if($conn=~/(\d+)\s+(\d+)\s+\d\s+\d\s+\d\s+\d/)
{
$c1=$1; $c2=$2;
#print"$c1 , $c2\n";
push @c1 , $c1;
push @c2, $c2;
}
}
$l = @c1;
foreach $i(0..$l-1)
{
 $dist=sqrt(($hash1{$c1[$i]}-$hash1{$c2[$i]})**2 +($hash2{$c1[$i]}-$hash2{$c2[$i]})**2 +($hash3{$c1[$i]}-$hash3{$c2[$i]})**2);
 print "$c1[$i]\t$c2[$i]\t$dist\n";
}
close F;
close G;




